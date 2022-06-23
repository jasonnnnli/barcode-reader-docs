---
layout: default-layout
title: Read Inverted Barcodes - Dynamsoft Barcode Reader SDK
description: This page describes how to read inverted barcodes in Dynamsoft Barcode Reader SDK.
keywords: Inverted Barcodes
needAutoGenerateSidebar: true
needGenerateH3Content: true
noTitleIndex: true
permalink: /programming/features/read-inverted-barcodes.html
---

# Read Inverted Barcodes

Generally, the barcode is dark on a light background. But in some situations, the barcodes are inverted - light barcodes on a dark background, as shown below.

<div align="center">
   <p><img src="assets/inverted-barcodes.png" width="70%" alt="inverted-barcodes"></p>
   <p>Inverted Barcodes</p>
</div>

Decoding inverted barcode is not enabled by default. To decode the inverted barcodes, you have to enable `GTM_INVERTED` in the `GrayscaleTransformationMode`.

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
// Add GTM_INVERTED to GrayscaleTransformationModes to decode inverted barcodes.
settings.furtherModes.grayscaleTransformationModes = [Dynamsoft.DBR.EnumGrayscaleTransformationMode.GTM_ORIGINAL, Dynamsoft.DBR.EnumGrayscaleTransformationMode.GTM_INVERTED];
// Update the settings.
await scanner.updateRuntimeSettings(settings);
```
>```java
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.getRuntimeSettings();
// Add GTM_INVERTED to GrayscaleTransformationModes to decode inverted barcodes.
settings.furtherModes.grayscaleTransformationModes = new int[]{EnumGrayscaleTransformationMode.GTM_ORIGINAL, EnumGrayscaleTransformationMode.GTM_INVERTED};
// Update the settings.
reader.updateRuntimeSettings(settings);
```
>```objc
NSError* err = nil;
// Obtain current runtime settings of `reader` instance.
iPublicRuntimeSettings* settings = [reader getRuntimeSettings:&err];
// Add GTM_INVERTED to GrayscaleTransformationModes to decode inverted barcodes.
settings.iFurtherModes.grayscaleTransformationModes = @[@(EnumGrayscaleTransformationModeOriginal),@(EnumGrayscaleTransformationModeInverted)];
// Update the settings.
[reader updateRuntimeSettings:settings error:&err];
```
>```swift
// Obtain current runtime settings of `barcodeReader` instance.
let settings = try? barcodeReader.getRuntimeSettings()
// Add GTM_INVERTED to GrayscaleTransformationModes to decode inverted barcodes.
settings.iFurtherModes.grayscaleTransformationModes = [EnumGrayscaleTransformationMode.original, EnumGrayscaleTransformationMode.inverted]
// Update the settings.
try? barcodeReader.updateRuntimeSettings(settings!)
```
>```c
PublicRuntimeSettings settings;
char szErrorMsg[256] = {0};
// Obtain current runtime settings of `reader` instance.
DBR_GetRuntimeSettings(reader, &settings);
// Add GTM_INVERTED to GrayscaleTransformationModes to decode inverted barcodes.
settings.furtherModes.grayscaleTransformationModes[0] = GTM_ORIGINAL;
settings.furtherModes.grayscaleTransformationModes[1] = GTM_INVERTED;
// Update the settings.
DBR_UpdateRuntimeSettings(reader, &settings, szErrorMsg, 256);
```
>```cpp
PublicRuntimeSettings settings;
char szErrorMsg[256] = {0};
// Obtain current runtime settings of `reader` instance.
reader.GetRuntimeSettings(&settings);
// Add GTM_INVERTED to GrayscaleTransformationModes to decode inverted barcodes.
settings.furtherModes.grayscaleTransformationModes[0] = GTM_ORIGINAL;
settings.furtherModes.grayscaleTransformationModes[1] = GTM_INVERTED;
// Update the settings.
reader.UpdateRuntimeSettings(&settings, szErrorMsg, 256);
```
>```c#
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.GetRuntimeSettings();
// Add GTM_INVERTED to GrayscaleTransformationModes to decode inverted barcodes.
settings.FurtherModes.GrayscaleTransformationModes[0] = GTM_ORIGINAL;
settings.FurtherModes.GrayscaleTransformationModes[1] = GTM_INVERTED;
// Update the settings.
reader.UpdateRuntimeSettings(settings);
```
>```java
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.getRuntimeSettings();
// Add GTM_INVERTED to GrayscaleTransformationModes to decode inverted barcodes.
settings.furtherModes.grayscaleTransformationModes = new int[]{EnumGrayscaleTransformationMode.GTM_ORIGINAL, EnumGrayscaleTransformationMode.GTM_INVERTED};
// Update the settings.
reader.updateRuntimeSettings(settings);
```
>```python
# Obtain current runtime settings of `reader` instance.
settings = reader.get_runtime_settings()
# Add GTM_INVERTED to GrayscaleTransformationModes to decode inverted barcodes.
settings.further_modes.grayscale_transformation_modes[0] = EnumGrayscaleTransformationMode.GTM_ORIGINAL
settings.further_modes.grayscale_transformation_modes[1] = EnumGrayscaleTransformationMode.GTM_INVERTED
# Update the settings.
reader.update_runtime_settings(settings)
```

**Remarks**

- When only `GTM_GENERAL` is enabled in `GrayscaleTransformationModes`, the barcode reader only scans general barcodes.
- When only `GTM_INVERTED` is enabled in `GrayscaleTransformationModes`, the barcode reader only scans inverted barcodes.
- When `GTM_GENERAL` is enabled as the first mode and `GTM_INVERTED` is enabled as the second mode in `GrayscaleTransformationModes`, the barcode reader will try to decode general barcodes first. If the count of decoded barcodes does not reach the expected number, the barcode reader will then try decoding the inverted barcodes.
