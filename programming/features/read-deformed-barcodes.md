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

<div align="center">
   <p><img src="assets/deformed-barcodes.png" width="80%" alt="deformed-barcodes"></p>
   <p>Deformed Barcodes</p>
</div>

DBR may not be able to handle such cases well by default, but you can configure the anti-deformation mode via parameter [`DeformationResistingModes`]({{ site.parameters_reference }}deformation-resisting-modes.html) to decode the deformed barcodes. Since DBR does not turn on anti-deformation modes by default, you need to add `DRM_GENERAL` to [`DeformationResistingModes`]({{ site.parameters_reference }}deformation-resisting-modes.html).

Multiple modes can also be set at the same time. For example, if DRM_SKIP and DRM_GENERAL are configured at the same time:

- The anti-deformation will not be enabled in the first round of barcode decoding
- If the decoded barcode results don't reach the number of `expectedBarcodeCount`, the anti-deformation will be enabled in the second round of barcode decoding.

If `DRM_GENERAL` of `DeformationResistingModes` still can't fulfill your requirements, you can try the following specific modes:

- `DRM_BROAD_WARP`: Resists deformation when the barcode is warped gently.
- `DRM_LOCAL_REFERENCE`: Resists deformation for barcodes with minor deformation in local modules.
- `DRM_DEWRINKLE`: Resists deformation for barcodes on a wrinkled surface.

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
// Add DRM_GENERAL to the deformationResistingModes to decode deformed barcodes.
settings.furtherModes.deformationResistingModes = [Dynamsoft.DBR.EnumDeformationResistingMode.DRM_GENERAL];
// Update the settings.
await scanner.updateRuntimeSettings(settings);
```
>```java
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.getRuntimeSettings();
// Add DRM_GENERAL to the deformationResistingModes to decode deformed barcodes.
settings.furtherModes.deformationResistingModes = new int[]{EnumDeformationResistingMode.DRM_GENERAL};
// Update the settings.
reader.updateRuntimeSettings(settings);
```
>```objc
NSError* err = nil;
// Obtain current runtime settings of `reader` instance.
iPublicRuntimeSettings* settings = [reader getRuntimeSettings:&err];
// Add DRM_GENERAL to the deformationResistingModes to decode deformed barcodes.
settings.iFurtherModes.deformationResistingModes = @[@(EnumDeformationResistingModeGeneral)];
// Update the settings.
[reader updateRuntimeSettings:settings error:&err];
```
>```swift
// Obtain current runtime settings of `barcodeReader` instance.
let settings = try? barcodeReader.getRuntimeSettings()
// Add DRM_GENERAL to the deformationResistingModes to decode deformed barcodes.
settings.iFurtherModes.deformationResistingModes = [EnumDeformationResistingMode.general]
// Update the settings.
try? barcodeReader.updateRuntimeSettings(settings!)
```
>```c
PublicRuntimeSettings settings;
char szErrorMsg[256] = {0};
// Obtain current runtime settings of `reader` instance.
DBR_GetRuntimeSettings(reader, &settings);
// Add DRM_GENERAL to the deformationResistingModes to decode deformed barcodes.
settings.furtherModes.deformationResistingModes[0] = DRM_GENERAL;
// Update the settings.
DBR_UpdateRuntimeSettings(reader, &settings, szErrorMsg, 256);
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
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.GetRuntimeSettings();
// Add DRM_GENERAL to the deformationResistingModes to decode deformed barcodes.
settings.FurtherModes.DeformationResistingModes[0] = DRM_GENERAL;
// Update the settings.
reader.UpdateRuntimeSettings(settings);
```
>```java
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.getRuntimeSettings();
// Add DRM_GENERAL to the deformationResistingModes to decode deformed barcodes.
settings.furtherModes.deformationResistingModes = new int[]{EnumDeformationResistingMode.DRM_GENERAL};
// Update the settings.
reader.updateRuntimeSettings(settings);
```
>```python
# Obtain current runtime settings of `reader` instance.
settings = reader.get_runtime_settings()
# Add DRM_GENERAL to the deformationResistingModes to decode deformed barcodes.
settings.further_modes.deformation_resisting_modes[0] = EnumDeformationResistingMode.DRM_GENERAL
# Update the settings.
reader.update_runtime_settings(settings)
```

> Note:
>
> `DeformationResistingModes` only works for QR Code and DataMatrix codes.