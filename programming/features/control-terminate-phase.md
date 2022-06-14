---   
layout: default-layout
title: Control the termination phase of DBR
description: This article describes how to use runtime settings to make DBR terminate at a certain stage.
keywords: terminate timeout
needAutoGenerateSidebar: false
breadcrumbText: Termination Control
---

# Control when to terminate a decoding process

Typically, DBR will terminate a decoding process after the barcode is decoded or the process has failed. In some cases we may want the process to terminate early. To do this, we use either the parameter [ `TerminatePhase` ]({{ site.parameters_reference }}terminate-phase.html) or the parameter [ `Timeout` ]({{ site.parameters_reference }}time-out.html). The former specifies the stage to terminate the process, the latter specifies the maximum time allowed for the process.

## TerminatePhase

This parameter can specify a certain stage to terminate the decoding. The main stages are:

* Region pre-detection
* Image preprocessing
* Image binarization
* Barcode localization
* Barcode type identification
* Barcode decoding/recognition  

By default, the decoding process will only terminate after all these stages are completed. To terminate early, assign one of the first 5 values to [ `TerminatePhase` ]({{ site.parameters_reference }}terminate-phase.html) in the following table:

|Enumeration name|Notes|
|---|----|
|TP_REGION_PREDETECTED | Terminate after the barcode region is pre-detected. |
|TP_IMAGE_PREPROCESSED | Terminate after the image is preprocessed. |
|TP_IMAGE_BINARIZED | Terminate after the image is binarized. |
|TP_BARCODE_LOCALIZED | Terminate after the barcode zone is localized. |
|TP_BARCODE_TYPE_DETERMINED | Terminate after the barcode type is identified. |
|TP_BARCODE_RECOGNIZED | Terminate after the barcode is recognized, the default value. |

After the termination, we can acquire information generated in the process as `Intermediate Results` which include the following:

> Note that for the JavaScript Edition, the intermediate result is only available when it is presented as an image.

| Enumeration name | Notes | Available in JavaScript Edition |
| IRT_NO_RESULT  | No information at all. | NA |
| IRT_ORIGINAL_IMAGE  | The original image processed by the barcode reader. | Yes |
| IRT_COLOUR_CONVERTED_GRAYSCALE_IMAGE  | Converted grayscale image based on the original image. | Yes |
| IRT_TRANSFORMED_GRAYSCALE_IMAGE  | Transformed grayscale image (e.g. color inversion). | Yes |
| IRT_PREDETECTED_REGION  | The coordinates of the predetected region. | No |
| IRT_PREPROCESSED_IMAGE  | The preprocessed image. | Yes |
| IRT_BINARIZED_IMAGE  | The binarized image. | Yes |
| IRT_TEXT_ZONE  | Coordinates of the zones of text found on the image. | No |
| IRT_CONTOUR  | Contours found on the image that surrounds different areas on the image. | No |
| IRT_LINE_SEGMENT  | Detected line segments. | No |
| IRT_TYPED_BARCODE_ZONE  | Coordinates of the barcode zones with determined barcode type(s). | No |
| IRT_PREDETECTED_QUADRILATERAL  | Coordinates of the predetected quadrilaterals. | No |

The following code illustrates how it's done:

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
```html
<div id='scannerV' style="width:50vw;height:50vh"></div>
<div id='cvses'></div>
<script>
// display intermediate result canvases
(async () => {
    let scanner = await Dynamsoft.DBR.BarcodeScanner.createInstance();
    document.getElementById('scannerV').appendChild(scanner.getUIElement());
    let rs = await scanner.getRuntimeSettings();
    // Specify which results you'd like to show
    rs.intermediateResultTypes = Dynamsoft.DBR.EnumIntermediateResultType.IRT_ORIGINAL_IMAGE | Dynamsoft.DBR.EnumIntermediateResultType.IRT_BINARIZED_IMAGE;
    await scanner.updateRuntimeSettings(rs);
    scanner.onUniqueRead = async (txt, result) => {
        try {
            // Show the intermediate results (images drawn in canvases)
            let cvss = await scanner.getIntermediateCanvas();
            for (let cvs of cvss) {
                document.getElementById('cvses').appendChild(cvs);
            }
            scanner.destroyContext();
        } catch (ex) {
            console.error(ex);
        }
    };
    await scanner.show();
})();
</script>
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
NOT SURE C++
```
>```c
NOT SURE C
```

>AGO

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
