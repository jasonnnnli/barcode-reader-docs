---   
layout: default-layout
description: This article introduces two ways to configure DBR, RuntimeSettings and Json template, and their syntax rules.
title: Use a template over RuntimeSettings
keywords: DBR RuntimeSettings Json Template ImageParameter FormatSpecification
needAutoGenerateSidebar: false
---

# Use a template over RuntimeSettings

DBR provides two ways for configuration: via `RuntimeSettings` or via a JSON template.

* [RuntimeSettings](#runtimesettings)

  `RuntimeSettings` is an object that manages various parameters during runtime. If you need to *dynamically* configure the reading process, use `RuntimeSettings`.

  However, bear in mind that `RuntimeSettings` doesn't provide all the available configuration options of the SDK.

* [JSON template](#json-template)

  With a JSON template, you can make use of all the configuration options that DBR offers.
  
  However, compared with `RuntimeSettings`, a template is static and can't be changed. If you need to use different settings for different scenarios, you can define a few templates and specify the proper one to use at runtime.

> It's also possible to use a template along with `RuntimeSettings`. Typically, you initialize the SDK with a template, the settings in which will be reflected in the runtime `RuntimeSettings`, then you can further fine-tune `RuntimeSettings` to apply to the actual reading process.

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
Dynamsoft.DLR.LabelRecognizer.license = 'YOUR-LICENSE-KEY';
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
NOT SURE JAVA-ANDROID
```
>
```objc
NOT SURE OBJC
```
>
```swift
NOT SURE SWIFT
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
reader->InitLicense("type your license");
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

## JSON template

DBR also supports managing parameters via JSON configuration files. This method is suitable for cases where the parameter configurations are relatively fixed. The JSON template mainly includes:

- `ImageParameter`: Defines the global configurations used for the entire image.
- `FormatSpecification`: Defines the configurations used for a particular barcode format. 
- `RegionDefinition`: Defines the configurations for a specific area of the image. 

### ImageParameter   

`ImageParameter` defines the global configurations used for the entire image. 

You can define one or multiple `ImageParameter`. When defining multiple `ImageParameter`, use `ImageParameterContentArray` and specify a different `Name` for each `ImageParameter` object. 

To use the `ImageParameter` configuration defined in the JSON template:

1. Use `InitRuntimeSettingsWithFile` to load a JSON file, or use `InitRuntimeSettingsWithString` to load a JSON string.
2. When calling DBR decoding functions, specify the configurations through `Name` of `ImageParameter`. 
  If not specified, the default `ImageParameter` configuration object will be used. 

The `emSettingPriority` parameters in the `InitRuntimeSettingsWithFile` and `InitRuntimeSettingsWithString` interfaces are used to specify how to operate the default configuration of the DBR when loading the JSON configuration. 

- If set to `CM_IGNORE`, the default configuration will not be changed. 
- If set to `CM_OVERWRITE`, the `ImageParameter` configuration you just loaded will be used and the default template will be merged. 

Below is a sample JSON template. In this example, we use the parameter `pTemplateName` of `DecodeFile` to specify the `ImageParameter` whose `Name` is "IP1".

```json
// One ImageParameter example 
{
    "Version": "3.0",
    "ImageParameter": {                   
        "Name": "IP1",
        "Description": "This is an imageParameter", 
        "BarcodeFormatIds": ["BF_ALL"]
     }
}
```
```json
//Multiple ImageParameter example 
{
    "Version": "3.0", 
    "ImageParameterContentArray": [                        
        {
            "Name": "IP1",              
            "BarcodeFormatIds": ["BF_ALL"]
        }, 
        {
            "Name": "IP2",                
            "BarcodeFormatIds": ["BF_CODE_39"]
        }, 
        {
            "Name": "IP3",                  
            "BarcodeFormatIds": ["BF_CODE_128"]
        }
    ]
}
``` 

```c++
CBarcodeReader* reader = new CBarcodeReader();         
reader->InitLicense("type your license");        
int ret; 
char sError[512];         
ret = reader->InitRuntimeSettingsWithFile("JsonTemplate.json",CM_OVERWRITE,
sError,512); ///Load a template configuration 
reader->DecodeFile("type your file path", "ImageParameter1"); //Use the configuration with the Name "IP1"    
TextResultArray* paryResult = NULL;         
reader->GetAllTextResults(&paryResult); //get decode result     
dynamsoft::dbr::CBarcodeReader::FreeTextResults(&paryResult);         
delete runtimeSettings;         
delete reader;
```

### FormatSpecification

If you only want to configure certain parameters for a specific pattern, then `FormatSpecification` should be used. This object defines the configuration used for a specific barcode format. 

If the configurations are inconsistent with the global `ImageParameter` configurations, then `FormatSpecification` has a higher priority. For specific configurable parameters and applicable scenarios, please refer to our documentation for [specific barcode format configuration parameters][2]. 

In JSON, use the `FormatSpecificationArray` to define one or multiple `FormatSpecification` objects, which can be distinguished by different `Name`. 
 
In the following example, we defines a `FormatSpecification` named "FS_1". 

```json
{
    "ImageParameter": {
        "Name": "ImageParameter1",
        "FormatSpecificationNameArray": ["FS_1"]
    }, 
    "FormatSpecificationArray": [
        {
            "Name": "FS_1",
            "AllmoduleDeviation": 10, 
            "BarcodeFormatIds": ["BF_CODE_39"]
        }
    ],
    "Version": "3.0"
}
```

### RegionDefinition

If you only care about a specific area on the image instead of the entire image or you want to make additional configurations for a specific area of the image, you can use `RegionDefinition`. Specifying the interested area can help DBR narrow the range of the image to be processed which helps increase the speed. 

The `RegionDefinition` object defines the configurations for the specified area of the image. If the configurations are inconsistent with the global `ImageParameter`  configurations, then the `RegionDefinition` has a higher priority. For specific configurable parameters, please refer to our [detailed documentation][1] on `RegionDefinition` . 

In JSON, one or more `RegionDefinitionArray` are defined by `RegionDefinitionArray` and distinguished by different `Name`.  

In the following example, we define two `RegionDefinition`, "RP_1" and "RP_2". 

```json
{
    "ImageParameter": {
        "Name": "ImageParameter1",
        "Description": "This is a region template", 
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
            "MeasuredByPercentage": 1
        }, 
        {
            "Name": "RP_2",
            "BarcodeFormatIds": ["BF_CODE_93"]
        }
    ], 
    "Version": "3.0"
}
```

[1]:manually-define-region-of-interest.html
[2]:format-specification.html



