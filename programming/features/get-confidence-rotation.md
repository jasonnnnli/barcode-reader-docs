---
layout: default-layout
title: How to Get Barcode Confidence and Angle
description: This page shows how to get barcode confidence and angle.
keywords: angle, confidence, decode result, how-to guides
needAutoGenerateSidebar: false
---

# How to Get Barcode Confidence and Rotation Angle

This article offers two examples about how to get result confidence and barcode rotation angle.

## Barcode Confidence

The score of recognition confidence could measure the reliability of a recognized result. The higher the score, the more precise the results are. 

## Barcode Rotation Angle

Dynamsoft Barcode Reader SDK is able to detect barcodes at all angles. The SDK is also able to return the angles of the barcodes decoded.

The following illustrations will show how the angle is calculated for different barcode types:

1. OneD Barcode
    ![OneD Barcode Rotation Angle][1]

2. QR Code
    ![QR Code Rotation Angle][2]

3. Data Matrix
    ![Data Matrix Rotation Angle][3]

4. Aztec
    ![Aztec Rotation Angle][4]

5. Maxicode
    ![Maxicode Rotation Angle][5]

## Code Snippet for Getting Confidence and Angle

The following code snippet shows how to get the confidence and rotation angle of the barcode result:

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
        cout << "Result " << j + 1 << endl;
        cout << "Confidence: " << barcodeResultItem->GetConfidence() << endl;
        cout << "Angle: " << barcodeResultItem->GetAngle() << endl;
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
            int confidence = item.getConfidence();
            Log.i("DecodedBarcodes", "The confidence of the barcode is: "+confidence);
            int angle = item.getAngle();
            Log.i("DecodedBarcodes", "The rotation angle of the barcode is: "+angle);
        }
    }
}
```
>
```objc
- (void)onDecodedBarcodesReceived:(DSDecodedBarcodesResult *)result {
    if (result.items.count > 0) {
        for (DSBarcodeResultItem *item in result.items) {
            NSInteger confidence = item.confidence;
            NSInteger angle = item.angle;
        }
    }
}
```
>
```swift
func onDecodedBarcodesReceived(_ result: DecodedBarcodesResult) {
    if let items = result.items, items.count > 0 {
        for item in items {
            let confidence = item.confidence
            let angle = item.angle
        }
    }
}
```

[1]: assets/get-confidence-rotation/1d-angle.png

[2]: assets/get-confidence-rotation/qr-angle.png

[3]: assets/get-confidence-rotation/dm-angle.png

[4]: assets/get-confidence-rotation/aztec-angle.png

[5]: assets/get-confidence-rotation/maxicode-angle.png
