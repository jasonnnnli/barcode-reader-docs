---
layout: default-layout
title: Read Image from Different Sources - Dynamsoft Barcode Reader SDK
description: This page describes how to read image from different sources in Dynamsoft Barcode Reader SDK.
keywords: Different Source
needAutoGenerateSidebar: true
needGenerateH3Content: true
noTitleIndex: true
---

# Read Barcode from Different Image Sources

The DBR algorithm provides multiple ways to read images from different sources. This article will introduce the following methods.

- Read from File
- Read from Memory

## Read from File

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
```
>```java
try{
   TextResult[] result = reader.decodeFile(Environment.getExternalStorageDirectory().toString()+"your file path");
} catch (BarcodeReaderException ex) {
   ex.printStackTrace();
}
```
>```objc
NSArray<iTextResult*>* barcodeResults = [barcodeReader decodeFileWithName:@"your file path" error:&error];
```
>```swift
let barcodeResults = try? barcodeReader.decodeFileWithName("your file path")
```
>```c
int errorCode = DBR_DecodeFile(barcodeReader, "C:\\Program Files (x86)\\Dynamsoft\\{Version number}\\Images\\AllSupportedBarcodeTypes.tif", "");
```
>```c++
int errorCode = reader->DecodeFile("C:\\Program Files (x86)\\Dynamsoft\\{Version number}\\Images\\AllSupportedBarcodeTypes.tif", "");
```
>```c#
try{
   TextResult[] result = reader.DecodeFile(@"C:\Program Files (x86)\Dynamsoft\{Version number}\Images\AllSupportedBarcodeTypes.tif", "");
} catch (BarcodeReaderException exp) {
   Console.WriteLine(exp.Message);
}
```
>```java
try{
   TextResult[] result = reader.decodeFile("your file path", "");
} catch (BarcodeReaderException ex) {
   ex.printStackTrace();
}
```
>
```python
try:
   results = dbr.decode_file(image_path)
   except BarcodeReaderError as bre:
      print(bre)
```

## Read File in Memory

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
```
>```java
try{
} catch (BarcodeReaderException ex) {
   ex.printStackTrace();
}
```
>```objc
UIImage *image = [[UIImage alloc] init];
NSArray<iTextResult*>* barcodeResults = [_barcodeReader decodeImage:image error:nil];
```
>```swift
let frameImage = dce.getFrameFromBuffer(true).toUIImage()
let barcodeResults = try? barcodeReader.decodeImage(frameImage)
```
>```c
```
>```c++
```
>```c#
try{
} catch (BarcodeReaderException exp) {
   Console.WriteLine(exp.Message);
}
```
>```java
private static byte[] getFileBytes(String filePath) {
   byte[] buffer = null;
   FileInputStream fis = null;
   ByteArrayOutputStream bos = null;
   try {
      fis = new FileInputStream(new File(filePath));
      bos = new ByteArrayOutputStream();
      byte[] tempBuffer = new byte[1024];
      int iReadSize;
      while ((iReadSize = fis.read(tempBuffer)) != -1) {
         bos.write(tempBuffer, 0, iReadSize);
      }
      buffer = bos.toByteArray();
   } catch (IOException ex) {
      ex.printStackTrace();
   } finally {
      if (null != bos) {
         try {
            bos.close();
         } catch (IOException e) {
            e.printStackTrace();
         }
      }
      if (null != fis) {
         try {
            fis.close();
         } catch (IOException e) {
            e.printStackTrace();
         }
      }
   }
   return buffer;
}
byte[] bytes = getFileBytes(filePath);
try{
   TextResult[] result = reader.decodeFileInMemory(bytes, "");
} catch (BarcodeReaderException ex) {
   ex.printStackTrace();
}
```
>
```python
# 3.2 Decoding with file bytes array
with open(image_path,"rb") as f:
    bytes = f.read()
results = dbr.decode_file_stream(bytearray(bytes))
```

Swift



## Read from Memory

```python
# Decoding with opencv image.
# Convert an image to a cv buffer.
cv_buffer = cv2.imread("The file path of the image")
# Use DBR decode_buffer to decode the buffered image.
results = dbr.decode_buffer(cv_buffer)
```

```java
private static ImageData cvtToImageData(String filePath) throws FileNotFoundException, IOException {
    BufferedImage in = ImageIO.read(new FileInputStream(filePath));
    BufferedImage image = new BufferedImage(in.getWidth(), in.getHeight(), BufferedImage.TYPE_3BYTE_BGR);
    Graphics2D graphics = image.createGraphics();
    graphics.drawImage(in, null, 0, 0);
    graphics.dispose();
    // calculate stride (c)
    int stride = ((24 * image.getWidth() + 31) / 32) * 4;
    ByteArrayOutputStream output = new ByteArrayOutputStream(image.getHeight() * stride);
    // Output rows bottom-up (b)
    Raster raster = image.getRaster().createChild(0, 0, image.getWidth(), image.getHeight(), 0, 0, new int[]{2, 1, 0});
    byte[] row = new byte[stride];
    for (int i = 0; i < image.getHeight(); i++) {
        row = (byte[]) raster.getDataElements(0, i, image.getWidth(), 1, row);
        output.write(row);
    }
    ImageData imgData = new ImageData();
    imgData.width = image.getWidth();
    imgData.height = image.getHeight();
    imgData.bytes = output.toByteArray();
    imgData.stride = stride;
    imgData.format = EnumImagePixelFormat.IPF_BGR_888;  
    return imgData;
}
ImageData img = cvtToImageData(filePath);
try {
    TextResult[] results = dbr.decodeBuffer(img.bytes, img.width, img.height, img.stride, img.format, "");
} catch (BarcodeReaderException ex){
    ex.printStackTrace();
} catch (IOException ex){
    ex.printStackTrace();
}
```

```objc
// MARK: - AVCaptureVideoDataOutputSampleBufferDelegate
- (void)captureOutput:(AVCaptureOutput *)output didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection {
   CVImageBufferRef imageBuffer = CMSampleBufferGetImageBuffer(sampleBuffer);
   if (imageBuffer == nil) {
      return;
   }
   CVPixelBufferLockBaseAddress(imageBuffer, 0);
   void *baseAddress = CVPixelBufferGetBaseAddress(imageBuffer);
   size_t bufferSize = CVPixelBufferGetDataSize(imageBuffer);
   size_t width = CVPixelBufferGetWidth(imageBuffer);
   size_t height = CVPixelBufferGetHeight(imageBuffer);
   size_t bytesPerRow = CVPixelBufferGetBytesPerRow(imageBuffer);
   CVPixelBufferUnlockBaseAddress(imageBuffer,0);
   NSData *buffer = [NSData dataWithBytes:baseAddress length:bufferSize];
   NSArray<iTextResult*> *result = [self.barcodeReader decodeBuffer:buffer withWidth:width height:height stride:bytesPerRow format:EnumImagePixelFormatARGB_8888 error:nil];
}
```

```swift
func captureOutput(_ output: AVCaptureOutput, didOutput sampleBuffer: CMSampleBuffer, from connection: AVCaptureConnection)
{
   let imageBuffer:CVImageBuffer = CMSampleBufferGetImageBuffer(sampleBuffer)!
   CVPixelBufferLockBaseAddress(imageBuffer, .readOnly)
   let baseAddress = CVPixelBufferGetBaseAddress(imageBuffer)
   let bufferSize = CVPixelBufferGetDataSize(imageBuffer)
   let width = CVPixelBufferGetWidth(imageBuffer)
   let height = CVPixelBufferGetHeight(imageBuffer)
   let bpr = CVPixelBufferGetBytesPerRow(imageBuffer)
   CVPixelBufferUnlockBaseAddress(imageBuffer, .readOnly)
   let buffer = Data(bytes: baseAddress!, count: bufferSize)
   guard let results = try? barcodeReader.decodeBuffer(buffer, width: width, height: height, stride: bpr, format: .ARGB_8888) else { return }   
}
```

```java
@Override
public void analyze(@NonNull ImageProxy imageProxy) {
   try {
      // insert your code here.
      // after done, release the ImageProxy object
      byte[] data = new byte[imageProxy.getPlanes()[0].getBuffer().remaining()];
      imageProxy.getPlanes()[0].getBuffer().get(data);
      int nRowStride = imageProxy.getPlanes()[0].getRowStride();
      int nPixelStride = imageProxy.getPlanes()[0].getPixelStride();
      try {
         TextResult[] results = mReader.decodeBuffer(data,
               nRowStride/nPixelStride, imageProxy.getHeight(), nRowStride,
               mImagePixelFormat);
         runOnUiThread(() -> {
            if(!isShowingDialog && results != null && results.length > 0) {
               showResult(results);
            }
         });
      } catch (BarcodeReaderException e) {
         e.printStackTrace();
      }
   } finally {
      imageProxy.close();
   }
}
```
