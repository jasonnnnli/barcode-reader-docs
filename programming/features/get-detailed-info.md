---
layout: default-layout
title: How to Get Detailed Barcode Information
description: This page shows how to get detailed barcode information.
keywords: additional information, OneDCodeDetails, QRCodeDetails, PDF417Details, DataMatrixDetails, AztecDetails
needAutoGenerateSidebar: false
---

# How to Get Detailed Barcode Information

The Dynamsoft Barcode Reader SDK provides APIs for you to get the detailed barcode information like checksum digit, start/stop characters, error correction level, etc. To learn more about what information you can get, see the following items:

- `OneDCodeDetails`: [C++]({{ site.cpp_api }}oned-code-details.html)
- `QRCodeDetails`: [C++]({{ site.cpp_api }}qr-code-details.html)
- `PDF417Details`: [C++]({{ site.cpp_api }}pdf417-details.html)
- `DataMatrixDetails`: [C++]({{ site.cpp_api }}datamatrix-details.html)
- `AztecDetails`: [C++]({{ site.cpp_api }}aztec-details.html)

Here we take QR Code as example and show how to get the version and model of a QR Code.

## What is the Version of a QR Code?

| QRCode Version | Modules |
|----------------|---------|
| Version 1 | 21 x 21 |
| Version 2 | 25 x 25 |
| ... | ... |
| Version N | (17 + N x 4) x (17 + N x 4) |
| Version 40 | 177 x 177 |

## What is the Model of a QR Code?

| QRCode Model | Description |
|--------------|---------|
| Model 1 | The original QR Code. It is a code capable of coding 1,167 numerals with its maximum version being 14 (73 x 73 modules). |
| Model 2 | Created by improving Model 1 so that this code can be read smoothly even if it is distorted in some way. This code can encode up to 7,089 numerals with its maximum version being 40 (177 x 177 modules). Today, the term QRCode usually refers to QRCode Model 2. |

## Code Snippet for Getting Detailed Barcode Information

<div class="sample-code-prefix template2"></div>
   >- C++
   >- Android
   >- Objective-C
   >- Swift
   >
>
```c++
CCaptureVisionRouter* cvr = new CCaptureVisionRouter;
CCapturedResult* result = cvr->Capture("IMAGE-FILE-PATH", CPresetTemplate::PT_READ_BARCODES);
if (result->GetErrorCode() != 0) {
    cout << "Error: " << result->GetErrorCode() << "," << result->GetErrorString() << endl;
}
int capturedResultItemCount = result->GetItemsCount();
for (int j = 0; j < capturedResultItemCount; j++) 
{
    const CCapturedResultItem* capturedResultItem = result->GetItem(j);
    CapturedResultItemType type = capturedResultItem->GetType();
    if (type == CapturedResultItemType::CRIT_BARCODE) 
    {
        const CBarcodeResultItem* barcodeResultItem = dynamic_cast<const CBarcodeResultItem*> (capturedResultItem);
        if (barcodeResultItem->GetFormat() == BarcodeFormat::BF_QR_CODE)
        {
            const CQRCodeDetails* detail = dynamic_cast<const CQRCodeDetails*>(barcodeResultItem->GetDetails());
            cout << "Version: " << detail->version;
            cout << "Model: " << detail->model;
        }
    }
}
// more process here
```
>
```java
public void onDecodedBarcodesReceived(DecodedBarcodesResult result) {
    if (result != null){
        BarcodeResultItem[] items = result.getItems();
        for (int i=0; i < items.length; i++){
            BarcodeResultItem item = items[i];
            Log.i("DecodedBarcodes", "onDecodedBarcodesReceived: This is the number "+i+" barcode");
            QRCodeDetails qrDetails = (QRCodeDetails) item.getDetails();
            int version = qrDetails.getVersion();
            Log.i("DecodedBarcodes", "The version of the QR barcode is: "+version);
            int model = qrDetails.getModel();
            Log.i("DecodedBarcodes", "The model of the QR barcode is: "+model);
        }
    }
}
```
>
```objc
- (void)onDecodedBarcodesReceived:(DSDecodedBarcodesResult *)result {
    if (result.items.count > 0) {
        for (DSBarcodeResultItem *item in result.items) {
            DSQRCodeDetails *qrDetails = (DSQRCodeDetails *) item.details;
            NSInteger version = qrDetails.version;
            NSInteger model = qrDetails.model;
        }
    }
}
```
>
```swift
func onDecodedBarcodesReceived(_ result: DecodedBarcodesResult) {
    if let items = result.items, items.count > 0 {
        for item in items {
            let qrCodeDetails = item.details as! QRCodeDetails
            let version = qrCodeDetails.version
            let model = qrCodeDetails.model
        }
    }
}
```
