---
layout: default-layout
title: Read Image from Different Sources - Dynamsoft Barcode Reader SDK
description: This page describes how to read images from different sources in Dynamsoft Barcode Reader SDK.
keywords: Different Source
needAutoGenerateSidebar: true
needGenerateH3Content: true
noTitleIndex: true
---

# Read Barcode from Different Image Sources

The DBR algorithm provides multiple ways to read images from different sources. This article will introduce the following methods.

- `DecodeFile`: Decode barcodes from a still image. You have to specify the file path when using this method to decode the barcodes.
- `DecodeFileInMemory`: Decode barcodes from an image file in memory.
- `DecodeBuffer`: Decode barcodes with buffered image data and the width, height, strides and pixel format of the image.

## DecodeFile

<div class="sample-code-prefix template2"></div>
   >- C
   >- C++
   >- C#
   >- Java
   >- Python
   >
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

## DecodeFileInMemory

`DecodeFileInMemory` is the method designed for decoding barcodes from the raw image data in bytes. The required parameters are as follows:

- `fileBytes`: The image data in bytes. It contains the image pixel data, pixel format and the size of the image.
- `templateName`: The barcode decoding template name.

<div class="sample-code-prefix template2"></div>
   >- C
   >- C++
   >- C#
   >- Java
   >- Python
   >
>```c
```
>```c++
```
>```c#
```
>```java
```
>
```python
```

## DecodeBuffer

`DecodeBuffer` is the method designed for decoding barcodes from the memory buffer containing image pixels in a defined format. This API is generally used in video stream decoding. After obtaining a frame of image data, you can invoke this API to decode the frame. The required parameters are as follows:

- BufferBytes: The array of bytes that contains the image data.
- Width: The width of the image (in pixel).
- Height: The height of the image (in pixel).
- Stride: The stride (or scan width) of the image.
- Format: The image pixel format used in the image byte array. View all available templates in `EnumImagePixelFormat`
- TemplateName: The template name. It indicates which barcode decoding template you are going to use when decoding the buffer.

<div class="sample-code-prefix template2"></div>
   >- C
   >- C++
   >- C#
   >- Java
   >- Python
   >
>```c
barcodeReader = DBR_CreateInstance();
int errorCode = DBR_DecodeBuffer(barcodeReader, pBufferBytes, iWidth, iHeight, iStride, format, "");
```
>```c++
int errorCode = reader->DecodeBuffer(pBufferBytes, iWidth, iHeight, iStride, format, "");
```
>```c#
Bitmap bBMP = new Bitmap(@"C:\Program Files (x86)\Dynamsoft\{Version number}\Images\AllSupportedBarcodeTypes.tif");
BitmapData bmdat = bBMP.LockBits(new Rectangle(Point.Empty, bBMP.Size), ImageLockMode.ReadOnly, PixelFormat.Format32bppArgb);
byte[] buffer = new byte[stride * bmdat.Height];
try{
   TextResult[] result = reader.DecodeBuffer(buffer, bBMP.Width, bBMP.Height, bmdat.Stride, EnumImagePixelFormat.IPF_ARGB_8888, "");
} catch (BarcodeReaderException exp) {
   Console.WriteLine(exp.Message);
}
```
>```java
ImageData image = cvtToImageData(filePath);
try {
   TextResult[] results = dbr.decodeBuffer(image.bytes, image.width, image.height, image.stride, image.format, "");
} catch (BarcodeReaderException ex){
   ex.printStackTrace();
} catch (IOException ex){
   ex.printStackTrace();
}
```
>
```python
# Decoding with opencv image.
# Convert an image to a cv buffer.
cv_buffer = cv2.imread("The file path of the image")
# Use DBR decode_buffer to decode the buffered image.
results = dbr.decode_buffer(cv_buffer)
```
