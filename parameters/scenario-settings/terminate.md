---   
layout: default-layout
title: Control the termination phase of DBR
description: This article describes how to use runtime settings to make DBR terminate at a certain stage.
keywords: terminate timeout
needAutoGenerateSidebar: false
breadcrumbText: Termination Control
---

# Control the termination of a decoding process

Typically, DBR will terminate a decoding process after the barcode is decoded or the process has failed. In some cases we may want the process to terminate early. To do this, we use either the parameter [ `TerminatePhase` ]({{ site.parameters_reference }}terminate-phase.html) or the parameter [ `Timeout` ]({{ site.parameters_reference }}time-out.html). The former specifies the stage to terminate the process, the latter specifies the maximum time allowed for the process.

## TerminatePhase

This parameter can specify a certain stage to terminate the decoding. The main stages are:

* Region pre-detection
* Image preprocessing
* Image binarization
* Barcode localization
* Barcode type identification
* Barcode decoding/recognition  

By default, the decoding process will only terminate after all these stages are completed. To terminate early, assign one of the following values to [ `TerminatePhase` ]({{ site.parameters_reference }}terminate-phase.html):

|Enumeration name|Note|
|---|----|
|TP_REGION_PREDETECTED|Terminate after Region Pre-detected|
|TP_IMAGE_PREPROCESSED|Terminate after Image Preprocessed|
|TP_IMAGE_BINARIZED|Terminate after Image binarized|
|TP_BARCODE_LOCALIZED|Terminate after Barcode localized|
|TP_BARCODE_TYPE_DETERMINED|Terminate after Barcode type identified|
|TP_BARCODE_RECOGENIZED|Terminate after Barcode recognized |

After the termination, use [ `IntermediateResult` ]({{ site.structs }}IntermediateResult.html) to obtain information from the process.

The following code snippets illustrat how it is done:

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
```javascript
// Obtain current runtime settings of `reader` instance.
let runtimeSettings = await scanner.getRuntimeSettings();
// Specify the barcode formats by enumeration values.
// The first group of barcode format (barcodeFormatIds) contains the majority of common barcode formats.
// Some special formats are listed in the second group (barcodeFormatIds_2).
runtimeSettings.barcodeFormatIds = Dynamsoft.DBR.EnumBarcodeFormat.BF_ONED | Dynamsoft.DBR.EnumBarcodeFormat.BF_QR_CODE;
// Update the settings.
await scanner.updateRuntimeSettings(runtimeSettings);
```
>
```java
NOT SURE
```
>
```objc
NOT SURE
```
>
```swift
NOT SURE
```
>
```python
NOT SURE
```
>
```java
NOT SURE
```
>
```c#
NOT SURE
```
>
```c++
char sError[512];
TextResultArray* paryResult = NULL;
PublicRuntimeSettings* runtimeSettings = new PublicRuntimeSettings();
CBarcodeReader* reader = new CBarcodeReader();
reader->InitLicense("input your license");
reader->GetRuntimeSettings(runtimeSettings); //Configure runtimesettings  
runtimeSettings->terminatePhase = TP_BARCODE_RECOGNIZED; //Specify terminate phase
reader->UpdateRuntimeSettings(runtimeSettings, sError, 512); //Update runtimesettings  
reader->DecodeFile("input your file path", ""); //Decoding
reader->GetAllTextResults(&paryResult); //Get results  
dynamsoft::dbr:: CBarcodeReader:: FreeTextResults(&paryResult);
delete runtimeSettings;
delete reader;
```
>```c
NOT SURE
```

## Timeout

This parameter will control the timeout for DBR algorithm in milliseconds, values ranging from[0, 0x7fffffff]. Default value is 10000. When DBR times out, it will terminate and return an error code related to the timeout. When dealing with multiple images, the user needs to consider a comprehensive timeout value to balance the trade-off between speed and accuracy for each image. The following code snippet illustrates how to set the [ `Timeout` ]({{ site.parameters_reference }}time-out.html):

```c++
char sError[512]; 
TextResultArray* paryResult = NULL; 
PublicRuntimeSettings* runtimeSettings = new PublicRuntimeSettings(); 
CBarcodeReader* reader = new CBarcodeReader(); 
reader->InitLicense("input your license"); 
reader->GetRuntimeSettings(runtimeSettings); //Configure runtimesettings   
runtimeSettings->timeout = 1000; //set timeout
reader->UpdateRuntimeSettings(runtimeSettings, sError, 512); //Update runtimesettings     
reader->DecodeFile("input your file path", ""); //Decoding  
reader->GetAllTextResults(&paryResult); //Get results     
dynamsoft::dbr:: CBarcodeReader:: FreeTextResults(&paryResult); 
delete runtimeSettings; 
delete reader; 

```

## Template

You could also set the [`TerminatePhase`]({{ site.parameters_reference }}terminate-phase.html)parameter via the JSON settings template. In the below JSON template, we set TerminatePhase to TP_BARCODE_LOCALIZED, so that the algorithm terminates once the barcode(s) are localized. In this case, the value of [`Timeout`]({{ site.parameters_reference }}time-out.html)is 1000, which means if the time consumed exceeds 1000 milliseconds, the DBR algorithm will terminate.
```json
{
    "ImageParameter": {
        "BarcodeFormatIds": ["BF_ALL"],
        "TerminatePhase":"TP_BARCODE_LOCALIZED",
        "Timeout": 1000
    },
    "Version": "3.0"
}
```
