---
layout: default-layout
title: Read Incomplete Barcodes - Dynamsoft Barcode Reader SDK
description: This page describes how to read incomplete barcodes in Dynamsoft Barcode Reader SDK.
keywords: Incomplete Barcodes
needAutoGenerateSidebar: true
needGenerateH3Content: true
noTitleIndex: true
---

# Read Incomplete Barcodes

In some case, due to misprinting, barcodes may have incomplete parts. For example, a QR code that is missing the position detection pattern (See the sample image below). In this case, you can enable the barcode completion logic in Dynamsoft Barcode Reader(DBR) by turning on [`BarcodeComplementModes`]({{ site.parameters_reference }}barcode-complement-modes.html). DBR will then automatically attempt to complete and correct the location information that is incorrect or lost due to misprinting according to the structure characteristics of the corresponding barcode type. The barcode completion logic only supports QR code and Data Matrix at present. `BarcodeComplementModes` is disabled by default, you can enable it based on your requirements.

Here are two examples with imcomplete barcodes  

![barcode-complememt-modes-sample-image-dm][1]
![barcode-complememt-modes-sample-image-qr][2]

**Code Snippet**

<div class="sample-code-prefix template2"></div>
   >- JavaScript
   >- Android
   >- Objective-C
   >- Swift
   >- C
   >- C++
   >- C#
   >- Java
   >- Python
   >
>```javascript
// Obtain current runtime settings of `reader` instance.
let settings = await scanner.getRuntimeSettings();
// Add BCM_GENERAL to the barcodeComplementModes to decode incomplete barcodes.
settings.furtherModes.deformationResistingModes = [Dynamsoft.DBR.EnumBarcodeComplementMode.BCM_GENERAL];
// Update the settings.
await scanner.updateRuntimeSettings(settings);
```
>```java
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.getRuntimeSettings();
// Add BCM_GENERAL to the barcodeComplementModes to decode incomplete barcodes.
settings.furtherModes.barcodeComplementModes = new int[]{EnumBarcodeComplementMode.BCM_GENERAL};
// Update the settings.
reader.updateRuntimeSettings(settings);
```
>```objc
NSError* err = nil;
// Obtain current runtime settings of `reader` instance.
iPublicRuntimeSettings* settings = [reader getRuntimeSettings:&err];
// Add BCM_GENERAL to the barcodeComplementModes to decode incomplete barcodes.
settings.iFurtherModes.barcodeComplementModes = @[@(EnumBarcodeComplementModeGeneral)];
// Update the settings.
[reader updateRuntimeSettings:settings error:&err];
```
>```swift
// Obtain current runtime settings of `barcodeReader` instance.
let settings = try? barcodeReader.getRuntimeSettings()
// Add BCM_GENERAL to the barcodeComplementModes to decode incomplete barcodes.
settings.iFurtherModes.barcodeComplementModes = [EnumBarcodeComplementMode.general]
// Update the settings.
try? barcodeReader.updateRuntimeSettings(settings!)
```
>```c
PublicRuntimeSettings settings;
char szErrorMsg[256] = {0};
// Obtain current runtime settings of `reader` instance.
DBR_GetRuntimeSettings(reader, &settings);
// Add BCM_GENERAL to the barcodeComplementModes to decode incomplete barcodes.
settings.furtherModes.barcodeComplementModes[0] = BCM_GENERAL;
// Update the settings.
DBR_UpdateRuntimeSettings(reader, &settings, szErrorMsg, 256);
```
>```cpp
PublicRuntimeSettings settings;
char szErrorMsg[256] = {0};
// Obtain current runtime settings of `reader` instance.
reader.GetRuntimeSettings(&settings);
// Add BCM_GENERAL to the barcodeComplementModes to decode incomplete barcodes.
settings.furtherModes.barcodeComplementModes[0] = BCM_GENERAL;
// Update the settings.
reader.UpdateRuntimeSettings(&settings, szErrorMsg, 256);
```
>```c#
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.GetRuntimeSettings();
// Add BCM_GENERAL to the barcodeComplementModes to decode incomplete barcodes.
settings.FurtherModes.BarcodeComplementModes[0] = BCM_GENERAL;
// Update the settings.
reader.UpdateRuntimeSettings(settings);
```
>```java
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.getRuntimeSettings();
// Add BCM_GENERAL to the barcodeComplementModes to decode incomplete barcodes.
settings.furtherModes.barcodeComplementModes = new int[]{EnumBarcodeComplementMode.BCM_GENERAL};
// Update the settings.
reader.updateRuntimeSettings(settings);
```
>```python
# Obtain current runtime settings of `reader` instance.
settings = reader.get_runtime_settings()
# Add BCM_GENERAL to the barcodeComplementModes to decode incomplete barcodes.
settings.further_modes.barcode_complement_modes[0] = EnumBarcodeComplementMode.BCM_GENERAL
# Update the settings.
reader.update_runtime_settings(settings)
```

[1]:assets\how-to-set-barcode-complememt-modes\barcode-complememt-modes-sample-image-dm.png
[2]:assets\how-to-set-barcode-complememt-modes\barcode-complememt-modes-sample-image-qr.png
