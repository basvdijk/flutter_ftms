# FTMS Flutter Plugin

This Flutter package allows you to connect to FTMS (Fitness Machine Service) devices via Bluetooth Low Energy (BLE). It provides functions for scanning for available devices, connecting to a specific device, and reading data and status information from the device.

⚠️ _**This Flutter package is currently under development.**_ ⚠️

## Supported Devices

| Device        | Implemented?           |
| ------------- | ---------------------- |
| Indoor Bike   | ✅ (implemented)       |
| Cross Trainer | 🚧 (under development) |

## Installation

Add the following dependency to your `pubspec.yaml` file:

```
dependencies:
  flutter_ftms:
    git:
      url: https://github.com/Malte2036/flutter_ftms.git
      ref: main
```

Then, run `flutter pub get` to install the package.

## Usage

Import the `flutter_ftms` package and use the `FTMS` class to interact with FTMS devices.

### Scanning for devices

You can scan for available FTMS devices using the `scanForBluetoothDevices()` function. This will start a scan and return a stream of `ScanResult` objects.

```
import 'package:flutter_ftms/flutter_ftms.dart';

await FTMS.scanForBluetoothDevices();
Stream<List<ScanResult>> scanResults = FTMS.scanResults;
```

### Connecting to a device

Once you have a `BluetoothDevice` object, you can connect to it using the `connectToFTMSDevice()` function.

```
import 'package:flutter_ftms/flutter_ftms.dart';

BluetoothDevice device = // obtain a BluetoothDevice object
await FTMS.connectToFTMSDevice(device);
```

### Reading data from a device

You can read data from an FTMS device using the `useDataCharacteristic()` function. This function takes a callback that will be called with an `FTMSData` object every time new data is received from the device.

```
import 'package:flutter_ftms/flutter_ftms.dart';

BluetoothDevice device = // obtain a BluetoothDevice object
await FTMS.useDataCharacteristic(device, (FTMSData data) {
    // handle new data
});
```

### Reading status information from a device

You can read status information from an FTMS device using the `useStatusCharacteristic()` function. This function does not take a callback, but instead updates an internal status object that can be accessed using the `readFeatureCharacteristic()` function.

```
import 'package:flutter_ftms/flutter_ftms.dart';

BluetoothDevice device = // obtain a BluetoothDevice object
await FTMS.useStatusCharacteristic(device);
FTMSFeature? feature = await FTMS.readFeatureCharacteristic(device);
if (feature != null) {
    // handle feature object
}
```

### Checking device type

You can check if a given Bluetooth device is an FTMS device using the `isBluetoothDeviceFTMSDevice()` function. This function returns a bool indicating whether or not the device supports the FTMS service.

```
import 'package:flutter_ftms/flutter_ftms.dart';

BluetoothDevice device = // obtain a BluetoothDevice object
bool isFTMSDevice = await FTMS.isBluetoothDeviceFTMSDevice(device);
```

### Getting device type

You can get the FTMS data type of a connected device using the `getFTMSDeviceType()` function. This function returns an `FTMSDataType` enum value indicating whether the device is an indoor bike or cross trainer.

```
import 'package:flutter_ftms/flutter_ftms.dart';

BluetoothDevice device = // obtain a BluetoothDevice object
FTMSDataType? dataType = await FTMS.getFTMSDeviceType(device);
if (dataType != null) {
    String deviceTypeString = FTMS.convertFTMSDataTypeToString(dataType);
    // handle device type
}
```
