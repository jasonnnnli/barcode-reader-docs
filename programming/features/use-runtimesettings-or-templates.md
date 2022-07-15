---   
layout: default-layout
description: This article introduces two ways to configure DBR, RuntimeSettings and Json template, and their syntax rules.
title: Use RuntimeSettings or Templates
keywords: DBR RuntimeSettings Json Template ImageParameter FormatSpecification
needAutoGenerateSidebar: true
needGenerateH3Content: true
noTitleIndex: true
permalink: /programming/features/use-runtimesettings-or-templates.html
---

# Use RuntimeSettings or Templates

DBR provides two ways for configuration: via `RuntimeSettings` or via a JSON template.

* [RuntimeSettings](#runtimesettings)

  `RuntimeSettings` is an object that manages various parameters during runtime. If you need to *dynamically* configure the reading process, use `RuntimeSettings`.

  However, bear in mind that `RuntimeSettings` doesn't provide all the available configuration options of the SDK.

* [JSON Templates](#json-template)

  With a JSON template, you can make use of all the configuration options that DBR offers.
  
  However, compared with `RuntimeSettings`, a template is static and can't be changed. If you need to use different settings for different scenarios, you can define a few templates and specify the proper one to use at runtime.

## RuntimeSettings

`RuntimeSettings` is an object that manages various runtime settings of the DBR SDK that determine how barcode reading is done. The following shows how to use it.

Basic steps:

1. Get the current value of the `RuntimeSettings` object
2. Change one or several settings
3. Update the `RuntimeSettings` object with the changed copy for the changes to take effect

The following code snippet demonstrates how to specify barcode formats with `RuntimeSettings`.  

<div class="sample-code-prefix template2"></div>
   >- Javascript
   >- Android
   >- Objective-C
   >- Swift
   >- Python
   >- Java
   >- C#
   >- C++
   >- C
   >
>
```javascript
// Specifies a license.
Dynamsoft.DBR.BarcodeScanner.license = 'YOUR-LICENSE-KEY';
// Creates a BarcodeScanner instance.
let scanner = await Dynamsoft.DBR.BarcodeScanner.createInstance();
// Obtains the current runtime settings.
let rs = await scanner.getRuntimeSettings();
// Sets the barcode format(s).
rs.barcodeFormatIds = Dynamsoft.DBR.EnumBarcodeFormat.BF_QR_CODE;
// Updates the settings.
await scanner.updateRuntimeSettings(rs);
```
>
```java
// Creates a BarcodeReader instance.
BarcodeReader reader = new BarcodeReader();
// Obtains the current runtime settings.
PublicRuntimeSettings rs = reader.getRuntimeSettings();
// Sets the barcode format(s).
rs.barcodeFormatIds = EnumBarcodeFormat.BF_QR_CODE;
// Updates the settings.
reader.updateRuntimeSettings(rs);
```
>
```objc
NSError* err = nil;
// Creates a BarcodeReader instance.
DynamsoftBarcodeReader* reader = [[DynamsoftBarcodeReader alloc] init];
// Obtains the current runtime settings.
iPublicRuntimeSettings* rs = [reader getRuntimeSettings:&err];
// Sets the barcode format(s).
rs.barcodeFormatIds = EnumBarcodeFormatQRCODE;
// Updates the settings.
[reader updateRuntimeSettings:rs error:&err];
```
>
```swift
// Creates a BarcodeReader instance.
let reader = DynamsoftBarcodeReader()
// Obtains the current runtime settings.
let rs = try? reader.getRuntimeSettings()
// Sets the barcode format(s).
rs?.barcodeFormatIds = EnumBarcodeFormatQRCODE
// Updates the settings.
try? reader.updateRuntimeSettings(rs)
```
>
```python
NOT SURE PYTHON
```
>
```java
NOT SURE JAVA
```
>
```c#
NOT SURE C#
```
>
```c++
// Creates a BarcodeReader instance.
CBarcodeReader* reader = new CBarcodeReader();
// Specifies a license.
reader->InitLicense("YOUR-LICENSE-KEY");
// Obtains the current runtime settings.
PublicRuntimeSettings* runtimeSettings = new PublicRuntimeSettings();
reader->GetRuntimeSettings(runtimeSettings);
// Sets the barcode format(s).
runtimeSettings->barcodeFormatIds = BF_QR_CODE;
char sError[512];
// Updates the settings.
reader->UpdateRuntimeSettings(runtimeSettings, sError, 512);
reader->DecodeFile("type your image path", "");
TextResultArray* paryResult = NULL;
// Gets the decoding results.
reader->GetAllTextResults(&paryResult);
dynamsoft::dbr::CBarcodeReader::FreeTextResults(&paryResult);
delete runtimeSettings;
delete reader;
```
>
```c
NOT SURE C
```

## JSON Templates

With a JSON template, you can make use of all the configuration options that DBR offers. A JSON template consists of three parts:

* `ImageParameter`: Defines the global configurations used for the entire image.
* `FormatSpecification`: Defines the configurations used for a particular barcode format.
* `RegionDefinition`: Defines the configurations for a specific area of the image.

> Read [Parameter Template Structure]({{ site.parameters }}structure-and-interfaces-of-parameters.md) to learn more about the structure of templates.

To use a template, you can either use `InitRuntimeSettingsWithFile` to load a JSON file, or use `InitRuntimeSettingsWithString`/`initRuntimeSettingsWithString` to load a JSON string.

> Notes about the JavaScript edition
>
> 1. It only supports importing a JSON string
> 2. It only allows one fixed template, in other words, the template itself should contain only one `ImageParameter` object 

The following code snippet demonstrates how to make use of a template.  

<div class="sample-code-prefix template2"></div>
   >- Javascript
   >- Android
   >- Objective-C
   >- Swift
   >- Python
   >- Java
   >- C#
   >- C++
   >- C
   >
>
```javascript
// Specifies a license.
Dynamsoft.DBR.BarcodeScanner.license = 'YOUR-LICENSE-KEY';
// Creates a BarcodeScanner instance.
let scanner = await Dynamsoft.DBR.BarcodeScanner.createInstance();
// Stringify a template into a string.
let template = JSON.stringify("A-JSON-Template");
// Updates the settings with the string.
await scanner.initRuntimeSettingsWithString(b);
```
>
```java
// Creates a BarcodeReader instance.
BarcodeReader reader = new BarcodeReader();
// Updates the settings with the string.
reader.initRuntimeSettingsWithString("A-JSON-Template");
```
>
```objc
NSError* err = nil;
// Creates a BarcodeReader instance.
DynamsoftBarcodeReader* reader = [[DynamsoftBarcodeReader alloc] init];
// Updates the settings with the string.
[reader initRuntimeSettingsWithString:@"A-JSON-Template" error:&err];
```
>
```swift
// Creates a BarcodeReader instance.
let reader = DynamsoftBarcodeReader()
// Updates the settings with the string.
try? reader.initRuntimeSettingsWithString("A-JSON-Template")
```
>
```python
NOT SURE PYTHON
```
>
```java
NOT SURE JAVA
```
>
```c#
NOT SURE C#
```
>
```c++
// Creates a BarcodeReader instance.
CBarcodeReader* reader = new CBarcodeReader();
char errorBuf[512];
dynamsoft::dbr::CBarcodeReader::InitLicense("YOUR-LICENSE-KEY", errorBuf, 512);
CBarcodeReader* reader = new CBarcodeReader();
char errorMessage[256];
// Initilizes the reader directly with the template in a file.
reader->InitRuntimeSettingsWithFile("{PATH-TO-YOUR-TEMPLATE}template.json", CM_OVERWRITE, errorMessage, 256);
```
>
```c
NOT SURE C
```

## Mixed Usage

It's also possible to use a template along with `RuntimeSettings`. Typically, you initialize the SDK with a template, the settings in which will be reflected in `RuntimeSettings`, then you can further fine-tune `RuntimeSettings` to apply to the actual reading process.
