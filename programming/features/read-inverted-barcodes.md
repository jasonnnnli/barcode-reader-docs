---
layout: default-layout
title: Read Inverted Barcodes - Dynamsoft Barcode Reader SDK
description: This page describes how to read inverted barcodes in Dynamsoft Barcode Reader SDK.
keywords: Inverted Barcodes
needAutoGenerateSidebar: true
needGenerateH3Content: true
noTitleIndex: true
---

# Read Inverted Barcodes

Generally, the barcode is dark on a light background. But in some situations, the barcodes are inverted - light barcodes on a dark background, as shown below.

![Dark Background Barcode][1]

Such kind of barcodes can be decoded if `GTM_INVERTED` of `GrayscaleTransformationMode` is enabled.

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
```
>```java
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.getRuntimeSettings();
// Update the GrayscaleTransformationModes, add GTM_INVERTED to the mode.
settings.furtherModes.grayscaleTransformationModes = new int[]{EnumGrayscaleTransformationMode.GTM_ORIGINAL, EnumGrayscaleTransformationMode.GTM_INVERTED};
// Update the settings.
reader.updateRuntimeSettings(settings);
```
>```objc
NSError* err = nil;
// Obtain current runtime settings of `reader` instance.
iPublicRuntimeSettings* settings = [reader getRuntimeSettings:&err];
settings.iFurtherModes.grayscaleTransformationModes = @[@(EnumGrayscaleTransformationModeOriginal),@(EnumGrayscaleTransformationModeInverted)];
// Update the settings.
[reader updateRuntimeSettings:settings error:&err];
```
>```swift
// Obtain current runtime settings of `barcodeReader` instance.
let settings = try? barcodeReader.getRuntimeSettings()
// Update the GrayscaleTransformationModes, add GTM_INVERTED to the mode.
settings.iFurtherModes.grayscaleTransformationModes = [EnumGrayscaleTransformationMode.original, EnumGrayscaleTransformationMode.inverted]
// Update the settings.
try? barcodeReader.updateRuntimeSettings(settings!)
```
>```c
```
>```cpp
PublicRuntimeSettings settings;
char szErrorMsg[256] = {0};
// Obtain current runtime settings of `reader` instance.
reader.GetRuntimeSettings(&settings);
// Update the GrayscaleTransformationModes, add GTM_INVERTED to the mode.
settings.furtherModes.grayscaleTransformationModes[0] = GTM_ORIGINAL;
settings.furtherModes.grayscaleTransformationModes[1] = GTM_INVERTED;
// Update the settings.
reader.UpdateRuntimeSettings(&settings, szErrorMsg, 256);
```
>```c#
```
>```java
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.getRuntimeSettings();
// Update the GrayscaleTransformationModes, add GTM_INVERTED to the mode.
settings.furtherModes.grayscaleTransformationModes = new int[]{EnumGrayscaleTransformationMode.GTM_ORIGINAL, EnumGrayscaleTransformationMode.GTM_INVERTED};
// Update the settings.
reader.updateRuntimeSettings(settings);
```
>```python
```

[1]: assets/read-barcodes-with-different-colors/dark-background-barcode.png
