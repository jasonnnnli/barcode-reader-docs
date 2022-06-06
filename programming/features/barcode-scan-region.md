---
layout: default-layout
title: Read a Specific Area/Region - Dynamsoft Barcode Reader SDK
description: This page describes how to read specific area or region in Dynamsoft Barcode Reader SDK.
keywords: Specific Area/Region
needAutoGenerateSidebar: true
needGenerateH3Content: true
noTitleIndex: true
---

# Read a Specific Area/Region

DBR will locate the code region and decode in the entire image by default. However, if only specific regions are required when decoding the barcode, you can define a Region Of Interest (ROI) by the parameter `RegionDefinition`. After defining a specific region, DBR will only decode barcodes within that region. Of course, this is very conducive to increasing the speed.

## Single Region Specification

`RegionDefinition` is the struct that designed to specify the ROI.

- `regionTop`: The y coordinate of the Top border of the region.
- `regionBottom`: The y coordinate of the Bottom border of the region.
- `regionLeft`: The x coordinate of the left border of the region.
- `regionRight`: The x coordinate of the right border of the region.
- `MeasureByPercentage`: If measured by percentage, the above values will be recognized as percentage (1 to 100). Otherwise, the above values will be recognized as pixel length.

You can either configure these settings via `PublicRuntimeSettings` struct or via a JSON template.

To update the setting via `PublicRuntimeSettings`:

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

settings.barcodeFormatIds = Dynamsoft.DBR.EnumBarcodeFormat.BF_ONED | Dynamsoft.DBR.EnumBarcodeFormat.BF_QR_CODE;
// Update the settings.
await scanner.updateRuntimeSettings(settings);
```
>```java
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.getRuntimeSettings();

settings.barcodeFormatIds = EnumBarcodeFormat.BF_QR_CODE | EnumBarcodeFormat.BF_ONED;
// Update the settings.
reader.updateRuntimeSettings(settings);
```
>```objc
NSError* err = nil;
// Obtain current runtime settings of `reader` instance.
iPublicRuntimeSettings* settings = [reader getRuntimeSettings:&err];

settings.barcodeFormatIds = EnumBarcodeFormatQRCODE | EnumBarcodeFormatONED;
// Update the settings.
[reader updateRuntimeSettings:settings error:&err];
```
>```swift
// Obtain current runtime settings of `barcodeReader` instance.
let settings = try? barcodeReader.getRuntimeSettings()

settings.barcodeFormatIds = EnumBarcodeFormat.ONED | EnumBarcodeFormat.QRCODE
// Update the settings.
try? barcodeReader.updateRuntimeSettings(settings!)
```
>```c
PublicRuntimeSettings settings;
char szErrorMsg[256] = {0};
// Obtain current runtime settings of `reader` instance.
DBR_GetRuntimeSettings(reader, &settings);

settings.barcodeFormatIds = BF_QR_CODE | BF_ONED;
// Update the settings.
DBR_UpdateRuntimeSettings(reader, &settings, szErrorMsg, 256);
```
>```c++
PublicRuntimeSettings settings;
char szErrorMsg[256] = {0};
// Obtain current runtime settings of `reader` instance.
reader.GetRuntimeSettings(&settings);

settings.barcodeFormatIds = BF_QR_CODE | BF_ONED;
// Update the settings.
reader.UpdateRuntimeSettings(&settings, szErrorMsg, 256);
```
>```c#
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.GetRuntimeSettings();

settings.BarcodeFormatIds = (int)(EnumBarcodeFormat.BF_QR_CODE | EnumBarcodeFormat.BF_ONED);
// Update the settings.
reader.UpdateRuntimeSettings(settings);
```
>```java
// Obtain current runtime settings of `reader` instance.
PublicRuntimeSettings settings = reader.getRuntimeSettings();

settings.barcodeFormatIds = EnumBarcodeFormat.BF_ONED | EnumBarcodeFormat.BF_QR_CODE;
// Update the settings.
reader.updateRuntimeSettings(settings);
```
>
```python
# Obtain current runtime settings of `reader` instance.
settings = reader.get_runtime_settings()

settings.barcode_format_ids = EnumBarcodeFormat.BF_ONED | EnumBarcodeFormat.BF_QR_CODE
# Update the settings.
reader.update_runtime_settings(settings)
```

JSON Template Example:

```json
{ 
   "ImageParameter": {
      "BarcodeFormatIds": ["BF_ALL"],
      "RegionDefinitionNameArray": ["RP_1", "RP_2"]
   }, 
   "RegionDefinition": {
      "Top": 10,
      "Bottom": 90,
      "Left": 10,
      "Right": 90,
      "MeasuredByPercentage": 1,
   },
   "Version": "3.0"
}
```

## Mulpitle Region Specification

If you are going to specify more than one ROI, you have to upload the settings via a JSON template.

```json
{ 
   "ImageParameter": {
      "BarcodeFormatIds": ["BF_ALL"],
      "RegionDefinitionNameArray": ["RP_1", "RP_2"]
   }, 
   "RegionDefinitionArray": [
      {
         "Name": "RP_1",   
         "BarcodeFormatIds": ["BF_CODE_39"],
         "Top": 20,         
         "Bottom": 80,      
         "Left": 20,        
         "Right": 80,      
         "ExpectedBarcodesCount": 10,
         "MeasuredByPercentage": 0
      }, 
      {
         "Name": "RP_2", 
         "BarcodeFormatIds": ["BF_CODE_93"], 
         "BarcodeFormatIds_2": ["BF_DOTCODE"], 
         "Top": 30, 
         "Bottom": 70, 
         "Left": 30, 
         "Right": 80, 
         "MeasuredByPercentage": 1
      }
   ], 
   "Version": "3.0"
}
```
