---
layout: default-layout
title: Read Deformed Barcodes - Dynamsoft Barcode Reader SDK
description: This page describes how to read deformed barcodes in Dynamsoft Barcode Reader SDK.
keywords: Deformed Barcode
needAutoGenerateSidebar: true
needGenerateH3Content: true
noTitleIndex: true
---

# Read Deformed Barcodes

As shown below, the barcodes on the surface of some flexible packaging or cylindrical objects tend to be distorted and deformed.

![Deformation sample image1][1]
![after deformation qr][3]
![Deformation sample image2][2]
![Deformation sample image2][4]

DBR may not be able to handle such cases well by default, but you can configure the anti-deformation mode via parameter [`DeformationResistingModes`]({{ site.parameters_reference }}deformation-resisting-modes.html) to decode the deformed barcodes. Since DBR does not turn on anti-deformation modes by default, you need to add `DRM_GENERAL` to [`DeformationResistingModes`]({{ site.parameters_reference }}deformation-resisting-modes.html). By the way, multiple modes can also be set at the same time. For example, if DRM_SKIP and DRM_GENERAL are configured at the same time:

- The anti-deformation will not be enabled in the first round of barcode decoding
- If the decoded barcode results doesn't reach the number of `expectedBarcodeCount`, the anti-deformation will be enabled in the second round of barcode decoding.

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
```
>```java
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.getRuntimeSettings();
// Add DRM_GENERAL to the deformationResistingModes to decode deformed barcodes.
settings.furtherModes.deformationResistingModes = new int[]{EnumBarcodeComplementMode.DRM_GENERAL};
// Update the settings.
reader.updateRuntimeSettings(settings);
```
>```objc
NSError* err = nil;
// Obtain current runtime settings of `reader` instance.
iPublicRuntimeSettings* settings = [reader getRuntimeSettings:&err];
// Add DRM_GENERAL to the deformationResistingModes to decode deformed barcodes.
settings.iFurtherModes.deformationResistingModes = @[@(EnumBarcodeComplementModeGeneral)];
// Update the settings.
[reader updateRuntimeSettings:settings error:&err];
```
>```swift
// Obtain current runtime settings of `barcodeReader` instance.
let settings = try? barcodeReader.getRuntimeSettings()
// Add DRM_GENERAL to the deformationResistingModes to decode deformed barcodes.
settings.iFurtherModes.deformationResistingModes = [EnumBarcodeComplementMode.general]
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
// Add DRM_GENERAL to the deformationResistingModes to decode deformed barcodes.
settings.furtherModes.deformationResistingModes[0] = DRM_GENERAL;
// Update the settings.
reader.UpdateRuntimeSettings(&settings, szErrorMsg, 256);
```
>```c#
```
>```java
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.getRuntimeSettings();
// Add DRM_GENERAL to the deformationResistingModes to decode deformed barcodes.
settings.furtherModes.deformationResistingModes = new int[]{EnumBarcodeComplementMode.DRM_GENERAL};
// Update the settings.
reader.updateRuntimeSettings(settings);
```
>```python
```

> Note:
>
> `DeformationResistingModes` only works for QR Code and DataMatrix codes.

[1]:assets\resist-deformation\resist-deformation-sample1.jpg
[2]:assets\resist-deformation\resist-deformation-sample2.png
[3]:assets\resist-deformation\after-drm-qr.png
[4]:assets\resist-deformation\after-drm-dm.png