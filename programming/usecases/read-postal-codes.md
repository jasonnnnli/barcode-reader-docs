---   
layout: default-layout
description: This article introduces how to read Postal codes.
title: How to read Postal codes
keywords: Postal code, Direct Part Marking
needAutoGenerateSidebar: true
needGenerateH3Content: true
noTitleIndex: true
permalink: /programming/features/read-postal-codes.html
---

# How to read Postal codes

## Sample Code

The following code snippet shows how to set the parameter via RuntimeSettings to read Postal code.

<div class="sample-code-prefix"></div>
>- JavaScript
>- C
>- C++
>- C#
>- Java
>- Android
>- Objective-C
>- Swift
>- Python
>
>1. 
```javascript
```
2. 
```c
```
3. 
```cpp
```
4. 
```csharp
```
5. 
```java
```
6. 
```java
BarcodeReader reader = new BarcodeReader();
PublicRuntimeSettings settings = reader.getRuntimeSettings(); //Get the current RuntimeSettings
settings.barcodeFormatIds = EnumBarcodeFormat.BF_NULL;
settings.barcodeFormatIds_2 = EnumBarcodeFormat_2.BF2_POSTALCODE;
reader.updateRuntimeSettings(settings); // Update RuntimeSettings with above setting
TextResult[] result = reader.decodeFile("YOUR-IMAGE-FILE-WITH-POSTAL-CODES"); // Start decoding
// Add further process
```
7. 
```objc
NSError* err = nil;
DynamsoftBarcodeReader *reader = [[DynamsoftBarcodeReader alloc] init];
iPublicRuntimeSettings *settings = [reader getRuntimeSettings:&err]; //Get the current RuntimeSettings
settings.barcodeFormatIds = EnumBarcodeFormatNULL;
settings.barcodeFormatIds_2 = EnumBarcodeFormat2POSTALCODE;
[reader updateRuntimeSettings:settings error:&err]; // Update RuntimeSettings with above setting
NSArray<iTextResult*>* result = [reader decodeFileWithName:@"YOUR-IMAGE-FILE-WITH-POSTAL-CODES" error:&err]; // Start decoding
// Add further process
```
8. 
```swift
let reader = DynamsoftBarcodeReader()
let settings = try? reader.getRuntimeSettings() //Get the current RuntimeSettings
settings?.barcodeFormatIds = EnumBarcodeFormat.NULL
settings?.barcodeFormatIds_2 = EnumBarcodeFormat2.POSTALCODE
try? reader.updateRuntimeSettings(settings) // Update RuntimeSettings with above setting
let result = try? reader.decodeFileWithName("YOUR-IMAGE-FILE-WITH-POSTAL-CODES") // Start decoding
// Add further process
```
9. 
```python

```
