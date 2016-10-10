# ACR Reactive BluetoothLE Plugin for Xamarin & Windows
Easy to use, cross platform, REACTIVE BluetoothLE Plugin for Xamarin (Windows UWP COMING SOON)

## PLATFORMS

* Android 4.3+
* iOS 6+
* tvOS / Mac (support is here, I haven't had the means to fully test these yet)
* Windows UWP (COMING SOON)

## FEATURES

* Scan for advertisement packets and devices
* Monitor adapter status
* Connect to device and monitor status
* Discover services, characteristics, & descriptors
* Read, write, & receive notifications for characteristics
* Read & write descriptors
* Monitor all aspects of the BLE plugin via CreateLogging extension
* Connect to heart rate monitors


## SETUP

Be sure to install the Acr.Ble nuget package in all of your main platform projects as well as your core/PCL project
[![NuGet](https://img.shields.io/nuget/v/Acr.Ble.svg?maxAge=2592000)](https://www.nuget.org/packages/Acr.Ble/)

**Android**

Add the following to your AndroidManifest.xml

```xml
<uses-permission android:name="android.permission.BLUETOOTH"/>
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>
```

**iOS**

If you want to use background BLE periperhals, add the following to your Info.plist

```xml    
<array>
<string>bluetooth-central</string>
</array>

To add a description to the Bluetooth request message (on iOS 10 this is required!)
```xml    
<key>NSBluetoothPeripheralUsageDescription</key>
<string>YOUR CUSTOM MESSAGE</string>
```


**Windows**

Add to your app manifest file
```xml
<Capabilities>
    <Capability Name="internetClient" />
    <DeviceCapability Name="bluetooth" />
</Capabilities>
```

## HOW TO USE BASICS

TODO

## DOCUMENTATION

* [Adapter](https://github.com/aritchie/bluetoothle/adapter.md)
* [Device](https://github.com/aritchie/bluetoothle/devices.md)
* [Services](https://github.com/aritchie/bluetoothle/services.md)
* [Characteristics](https://github.com/aritchie/bluetoothle/characteristics.md)
* [Descriptors](https://github.com/aritchie/bluetoothle/descriptors.md)
* Plugins
    * [Logging](https://github.com/aritchie/bluetoothle/logging.md)
    * [Heart Rate](https://github.com/aritchie/bluetoothle/heartrate.md)

## FAQ

Q. Why is everything reactive instead of events/async

> I wanted event streams as I was scanning devices.  I also wanted to throttle things like characteristic notification feeds.  Lastly, was the proper cleanup of events and resources.   

Q. Why are Device.Connect, Characteristic.Read, and Descriptor.Read observable when async would do just fine?

> True, but observables with RX are actually awaitable as well and far easier to chain into other things.

Q. Why have a Adapter.BackgroundScan with a service UUID?  This is not a problem on Android

> Also, true, but consistency is what I was aiming for.  iOS only allows you to scan in the background with a serviceUUID and on Android, I set the scanmode to low power.

Q. Why are devices cleared on a new scan?

> Some platforms yield a "new" device and therefore new hooks.  This was observed on some android devices.

Q. My characteristic read/writes/notifications are not working
> If you store your discovered characteristics in your own variables, make sure to refresh them with each (re)connect
