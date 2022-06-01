---
layout: default-layout
title: There are many editions of DBR, what are the differences? which one should I use?
keywords: Dynamsoft Barcode Reader, FAQ, DBR Introduction, General, editions
description: There are many editions of DBR, what are the differences? which one should I use?
needAutoGenerateSidebar: false
---

# FAQ - General

## What are the different DBR editions and how do I choose the one I need?

Based on the same algorithm, DBR is packaged into the following different editions depending on the language used:

* [JavaScript (Web)]({{site.js}}user-guide/)
* [Java (Android)]({{site.android}})
* [Object-C / Swift (iOS)]({{site.oc}})
* [Python (Windows, Linux, macOS)]({{site.python}})
* [Java (Windows, Linux, macOS)]({{site.java}})
* [C\# (Windows)]({{site.dotnet}})
* [C++ (Windows, Linux, macOS)]({{site.cpp}})
* [C (Windows, Linux, macOS)]({{site.c}})

You can choose one of the editions based on your application type and the language you intend to use:

* Web application: JavaScript edition
* Mobile application: Object-C / Swift edition | Java for Android edition
* Desktop application: Python | Java | C\# | C++ | C edition
* Desktop application: (embedded – e.g. raspberry pi): Windows/Linux edition
- native mobile app: iOS/Android edition
- webapp (server-side): Windows/Linux edition
- webapp (client-side): JavaScript edition

> Note - It is important to note the difference the Windows/Linux edition and the JavaScript edition when it comes to web applications. The Windows/Linux edition can only operate on the server-side, so it cannot offer live video decoding, while the JavaScript edition can since it is client-side.
