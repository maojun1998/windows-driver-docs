---
title: Videos Debugging UMDF Drivers
author: windows-driver-content
description: This topic contains a series of videos by Abhishek Ram that demonstrate how to debug User-Mode Driver Framework (UMDF) drivers.
Search.SourceType: Video
ms.assetid: 969FD292-5D92-4257-8E15-F2129B832E22
---

# Videos: Debugging UMDF Drivers


This topic contains a series of videos by Abhishek Ram that demonstrate how to debug User-Mode Driver Framework (UMDF) drivers.

After watching the videos, you'll be familiar with the UMDF debugger extensions and know how to use them in basic debugging scenarios.

While the videos demonstrate debugging a UMDF version 1 driver on older versions of Windows, you can still use the same techniques with a UMDF version 2 driver running on current versions of Windows.

**Note**  This video describes the debugger extension commands in Wudfext.dll, which you can use to debug UMDF version 1 drivers only. To debug UMDF drivers starting in UMDF version 2.0, you must instead use the Wdfkd.dll debugger extension library. There are equivalents in Wdfkd.dll for all of the extensions in Wudfext.dll. For more info, see [Summary of Debugger Extensions in Wudfext.dll](using-umdf-debugger-extensions.md) and [Summary of Debugger Extensions in Wdfkd.dll](debugger-extensions-for-kmdf-drivers.md).

 

For more information about debugging UMDF, see the topics listed in [Debugging WDF Drivers](debugging-a-wdf-driver.md).

## Prerequisites


To get the most from this content you should have working knowledge of UMDF and the Debugging Tools for Windows. Because each session builds on the previous one, we recommend that you view these demonstrations in the order listed.

## Basics and setup


Discusses use of the WDK samples and the OSR USB-FX2 Learning Kit.

<iframe src="https://hubs-video.ssl.catalog.video.msn.com/embed/d1040a16-81ec-40bb-a2d5-05021a37a144/IA?csid=ux-en-us&MsnPlayerLeadsWith=html&PlaybackMode=Inline&MsnPlayerDisplayShareBar=false&MsnPlayerDisplayInfoButton=false&iframe=true&QualityOverride=HD" width="720" height="405" allowFullScreen="true" frameBorder="0" scrolling="no">UMDF debugging video part 1</iframe>

In this video, you'll learn about UMDF debugging basics, including preparing your test machine, using the Devcon tool to install the UMDF Echo sample driver, using WdfVerifier to identify the host process hosting a given UMDF driver, and using WdfVerifier to attach the host process to the debugger in time to debug initialization code. This video also shows how you can list running host processes in Task Manager, and view running drivers in Device Manager.

## Examining the object hierarchy with debugger extensions


<iframe src="https://hubs-video.ssl.catalog.video.msn.com/embed/da033b03-b965-40cc-9697-ecb97430006a/IA?csid=ux-en-us&MsnPlayerLeadsWith=html&PlaybackMode=Inline&MsnPlayerDisplayShareBar=false&MsnPlayerDisplayInfoButton=false&iframe=true&QualityOverride=HD" width="720" height="405" allowFullScreen="true" frameBorder="0" scrolling="no">UMDF debugging video part 2a</iframe>

In this part, you'll learn how to start debugging a UMDF driver. The video describes how to set up the OSR USB-FX2 driver sample and application sample so that three instances of the app send read, write, and device I/O control requests to the driver. You'll see how the requests flow first to the reflector, and then to the user mode driver host process. This video introduces the WDF object hierarchy for the FX2 driver sample, and discusses how to use the following UMDF debugger extensions to traverse the UMDF object hierarchy:

-   [**!wudfext.umdevstacks**](https://msdn.microsoft.com/library/windows/hardware/ff566191)
-   [**!wudfext.wudfdriverinfo**](https://msdn.microsoft.com/library/windows/hardware/ff566207)
-   [**!wudfext.wudfdevice**](https://msdn.microsoft.com/library/windows/hardware/ff566199)
-   [**!wudfext.wudfdevicequeues**](https://msdn.microsoft.com/library/windows/hardware/ff566203)

For UMDF 2, see [Summary of Debugger Extensions in Wdfkd.dll](debugger-extensions-for-kmdf-drivers.md), for example [**!wdfkd.wdfumdevstacks**](https://msdn.microsoft.com/library/windows/hardware/dn265380).

## Accessing framework USB objects


<iframe src="https://hubs-video.ssl.catalog.video.msn.com/embed/f22577ab-1da0-47ae-b12b-ed3d586cde9e/IA?csid=ux-en-us&MsnPlayerLeadsWith=html&PlaybackMode=Inline&MsnPlayerDisplayShareBar=false&MsnPlayerDisplayInfoButton=false&iframe=true&QualityOverride=HD" width="720" height="405" allowFullScreen="true" frameBorder="0" scrolling="no">UMDF debugging video part 2b</iframe>

Here, you'll learn how to examine the driver's framework USB objects. To do so, you'll navigate through the WDF object hiearchy to reach the USB pipe objects, USB interface objects, and USB I/O target objects.

##  I/O requests and queues


<iframe src="https://hubs-video.ssl.catalog.video.msn.com/embed/48165551-a75d-4855-b0c8-3e55826f4f5e/IA?csid=ux-en-us&MsnPlayerLeadsWith=html&PlaybackMode=Inline&MsnPlayerDisplayShareBar=false&MsnPlayerDisplayInfoButton=false&iframe=true&QualityOverride=HD" width="720" height="405" allowFullScreen="true" frameBorder="0" scrolling="no">UMDF debugging video part 2c</iframe>

In this video, you'll use the debugger to examine the driver's framework I/O request objects and framework queue objects.

## File objects and callback objects


<iframe src="https://hubs-video.ssl.catalog.video.msn.com/embed/39c05ac7-3e20-4b8d-bcc9-37f450ddf507/IA?csid=ux-en-us&MsnPlayerLeadsWith=html&PlaybackMode=Inline&MsnPlayerDisplayShareBar=false&MsnPlayerDisplayInfoButton=false&iframe=true&QualityOverride=HD" width="720" height="405" allowFullScreen="true" frameBorder="0" scrolling="no">UMDF debugging video part 2d</iframe>

In this part, you'll learn how to examine framework file objects as well as the driver's callback objects.

##  Tracking I/O requests sent by a UMDF driver


<iframe src="https://hubs-video.ssl.catalog.video.msn.com/embed/8d1aa0a2-4360-4d68-9b09-310851a6087f/IA?csid=ux-en-us&MsnPlayerLeadsWith=html&PlaybackMode=Inline&MsnPlayerDisplayShareBar=false&MsnPlayerDisplayInfoButton=false&iframe=true&QualityOverride=HD" width="720" height="405" allowFullScreen="true" frameBorder="0" scrolling="no">UMDF debugging video part 3a</iframe>

Here, you'll learn how to use the App Verifier tool to help you debug. You'll also learn how to debug driver initialization code, and how to track requests sent by a UMDF driver to the kernel stack below.

##  Driver does not complete an I/O request


<iframe src="https://hubs-video.ssl.catalog.video.msn.com/embed/ddf4eff2-73f9-44a9-8602-adb08fc48373/IA?csid=ux-en-us&MsnPlayerLeadsWith=html&PlaybackMode=Inline&MsnPlayerDisplayShareBar=false&MsnPlayerDisplayInfoButton=false&iframe=true&QualityOverride=HD" width="720" height="405" allowFullScreen="true" frameBorder="0" scrolling="no">UMDF debugging video part 3b</iframe>

In the final video, you'll investigate a case when a UMDF driver does not complete a request it received, and you'll learn about the framework's object tracking and reference tracking capabilities.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bwdf\wdf%5D:%20Videos:%20Debugging%20UMDF%20Drivers%20%20RELEASE:%20%284/5/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



