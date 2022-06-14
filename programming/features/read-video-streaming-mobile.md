---
layout: default-layout
title: Read Barcode from Video Streaming - Dynamsoft Barcode Reader SDK
description: This page describes how to read barcodes from video streaming in Dynamsoft Barcode Reader SDK.
keywords: Different Source
needAutoGenerateSidebar: true
needGenerateH3Content: true
noTitleIndex: true
---

# Read Barcode from Video Streaming

## Configurations on the Camera

Firstly, to decode from video streaming, you have to create a camera module. The camera module is responsible for:

- Capturing the video streaming.
- Displaying the video streaming on the UI.
- Transfer the captured data to the barcode reader for barcode decoding.

<div class="sample-code-prefix template2"></div>
   >- Android
   >- Objective-C
   >- Swift
   >
>```java
public class MainActivity extends AppCompatActivity {
    CameraEnhancer mCameraEnhancer;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        DCECameraView cameraView = findViewById(R.id.cameraView);
        // Create an instance of Dynamsoft Camera Enhancer for video streaming.
        mCameraEnhancer = new CameraEnhancer(MainActivity.this);
        mCameraEnhancer.setCameraView(cameraView);
    }
}
```
>```objc
@property(nonatomic, strong) DynamsoftCameraEnhancer *dce;
@property(nonatomic, strong) DCECameraView *dceView;
- (void)configurationDCE{
   // Initialize a camera view for previewing video.
   _dceView = [DCECameraView cameraWithFrame:self.view.bounds];
   [self.view addSubview:_dceView];
   // Initialize the Camera Enhancer with the camera view.
   _dce = [[DynamsoftCameraEnhancer alloc] initWithView:_dceView];
}
```
>```swift
class ViewController: UIViewController {
   var dce:DynamsoftCameraEnhancer! = nil
   var dceView:DCECameraView! = nil
   func configurationDCE() {
      dceView = DCECameraView.init(frame: self.view.bounds)
      self.view.addSubview(dceView)
      // Initialize the Camera Enhancer with the camera view.
      dce = DynamsoftCameraEnhancer.init(view: dceView)
   }
}
```

## Configure Barcode Reader and Start Video Barcode Decoding

Initialize Dynamsoft Barcode Reader and bind the Camera Enhancer to the Barcode Reader.

<div class="sample-code-prefix template2"></div>
   >- Android
   >- Objective-C
   >- Swift
   >
>```java
public class MainActivity extends AppCompatActivity {
    BarcodeReader mBarcodeReader;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        ...
        try {
            // Create an instance of Dynamsoft Barcode Reader.
            mBarcodeReader = new BarcodeReader();
        } catch (BarcodeReaderException e) {
            e.printStackTrace();
        }
        // Bind the instance of Camera to the BarcodeReader
        mBarcodeReader.setCameraEnhancer(mCameraEnhancer);
    }
}
```
>```objc
@property(nonatomic, strong) DynamsoftBarcodeReader *barcodeReader;
...
- (void)configurationDBR{
   // Add function configureDBR and add the following code.
   _barcodeReader = [[DynamsoftBarcodeReader alloc] init];
   // Bind the instance of Camera to the BarcodeReader
   [_barcodeReader setCameraEnhancer:_dce];
}
```
>```swift
var barcodeReader:DynamsoftBarcodeReader! = nil
...
class ViewController: UIViewController {
   // Add function configureDBR and add the following code.
   func configurationDBR() {
      barcodeReader = DynamsoftBarcodeReader.init()
      // Bind the instance of Camera to the BarcodeReader
      barcodeReader.setCameraEnhancer(dce)
   }
}
```

Added `TextResultCallback` to receive the barcode results and then trigger the `startScanning`.

<div class="sample-code-prefix template2"></div>
   >- Android
   >- Objective-C
   >- Swift
   >
>```java
public class MainActivity extends AppCompatActivity {
   @Override
   protected void onCreate(Bundle savedInstanceState) {
      ...
      mReader.setTextResultListener(new TextResultListener() {
         // Obtain the recognized barcode results and display.
         @Override
         public void textResultCallback(int id, ImageData imageData, TextResult[] textResults) {
            // Add code to execute when barcode textResult is received.
         }
      });
   }
   @Override
   public void onResume() {
      mReader.startScanning();
      super.onResume();
   }
   @Override
   public void onPause() {
      mReader.stopScanning();
      super.onPause();
   }
}
```
>```objc
@interface ViewController ()<DBRTextResultListener>
...
- (void)configurationDBR{
   [_barcodeReader setDBRTextResultListener:self];
   [_barcodeReader startScanning];
}
- (void)textResultCallback:(NSInteger)frameId imageData:(iImageData *)imageData results:(NSArray<iTextResult *> *)results{
   // Add code to execute when barcode textResult is received.
}
```
>```swift
var barcodeReader:DynamsoftBarcodeReader! = nil
...
// Add DBRTextResultListener to the viewController
class ViewController: UIViewController, DBRTextResultListener {
   // Add function configureDBR and add the following code.
   func configurationDBR() {
      ...
      barcodeReader.setDBRTextResultListener(self)
      barcodeReader.startScanning()
   }
   func textResultCallback(_ frameId: Int, imageData: iImageData, results: [iTextResult]?) {
      // Add code to execute when barcode textResult is received.
   }
}
```
