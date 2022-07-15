---
layout: default-layout
title: Read Barcode from PDF files - Dynamsoft Barcode Reader SDK
description: This page describes how to read barcodes PDF files with Dynamsoft Barcode Reader SDK.
keywords: PDF, TIFF
needAutoGenerateSidebar: true
needGenerateH3Content: true
noTitleIndex: true
permalink: /programming/features/read-from-pdf.html
---

# Read Barcode from PDF files

Dynamsoft Barcode Reader provides specific parameters for processing PDF files. You can set which pages you are going to scan or modify the image processing modes of the PDF files.

## Page Specification

Parameter `Pages` is designed to specify which pages of the file should be processed when the given file has multiple pages (like a PDF file or a fax file in TIF). `Pages` is set via a string that includes page number or a range of pages. For example:

- If you set `Pages` to "1,3,5", the first, third and fifth pages will be processed.
- If you set `Pages` to "1, 3-6", the first page and pages 3 to 6 will be processed.

The Pages parameter must be uploaded via a JSON template. An example is shown as follows:

```json
{
    "ImageParameter": {
        ...
        "Pages": "1,2,3, 6-8"           
    }, 
    "Version": "3.0"
}
```

## PDF Processing Modes Configuration

`PDFReadingMode` and `PDFRasterDPI` are specially designed to handle the image processing of PDF files.

### PDFReadingMode

There are two modes provided to process different types of PDF files.

- `PDFRM_VECTOR`

  This method is specifically designed for PDF files composed of vector data. This mode will not render PDF data into images, but directly extract PDF vector data for barcode region positioning and decoding. Its advantages are fast speed and high accuracy, but it is only suitable for PDF files composed of vector data.

- `PDFRM_RASTER`

  This method will render each page of the PDF as an image, which will be processed later. If you are not sure whether the PDF files are composed of vector data, you can enable this method so that they can be transferred into raster images and processed. The drawback is that it is much slower than `PDFRM_VECTOR` when processing vector images.

At the same time, we also provide `PDFRM_AUTO` mode, this mode will automatically choose the appropriate processing mode according to whether the PDF file has enough available vector data

### PDFRasterDPI

When using `PDFRM_RASTER`, we need to select an appropriate `PDFRasterDPI` to ensure that the rendered image has the right size. The higher the `PDFRasterDPI`, the higher the final resolution of the rendered image. The high-resolution image can ensure the image details are not distorted, which is helpful for DBR to correctly identify the barcode region but will make the processing speed slow at the same time. This section will introduce the calculation method from `PDFRasterDPI` to the size of the rendered image. You can observe the rendered image based on the calculation method and the intermediate result `IRT_ORIGINAL_IMAGE` to decide how to adjust `PDFRasterDPI`.

The resolution of the rendered image is calculated as follows: Set PDF page height to h and page width to w, Final rendered image height ImgHeight = h / 72 * `PDFRasterDPI` Final rendered image width ImgWidth = w / 72 * `PDFRasterDPI`

`PDFRasterDPI` is the number of pixels per inch of the image. The page width and height unit defined in PDF is pt (length unit, 1 inch = 72 pt), so in the above formula, we first divide the width and height by 72 to get the inch length of the page and then multiply by `PDFRasterDPI` to get the final image pixel width and height.

## Sample Template

In the following template, we configured `PDFReadingMode` to `PDFRM_AUTO`, `PDFRasterDPI` to 500, and `Pages` we specified the pages with indexes of  1, 2, and 4 to 6.

```json
{
    "ImageParameter": {
        "BarcodeFormatIds": ["BF_ALL"], 
        "PDFRasterDPI": 500,
        "PDFReadingMode": {
            "Mode": "PDFRM_AUTO "
        },                         
        "Pages": "1,2,4-6"           
    }, 
    "Version": "3.0"
}
```
