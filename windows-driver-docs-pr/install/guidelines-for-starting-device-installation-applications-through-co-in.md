---
title: Guidelines for Starting Device Installation Applications through Co-installers
description: Guidelines for Starting Device Installation Applications through Co-installers
ms.assetid: 94b21eef-5660-4d05-8eb5-da6589c85e65
---

# Guidelines for Starting Device Installation Applications through Co-installers


The following guidelines must be followed for co-installers which supply [finish-install actions](finish-install-actions--windows-vista-and-later-.md) (Windows Vista and later versions of Windows) to start [*device installation applications*](https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-installation-application):

-   A co-installer must not exit from its finish-install pages or finish-install action until the device installation application has finished. If a co-installer exits early and another driver requires a restart, Windows might restart the computer before the application has completed.

-   A co-installer should first look for the device installation application on the distribution medium and, if the application is present, silently begin the installation process.

    If the distribution medium is not present, the co-installer should offer the user the choice of either inserting a medium or downloading the device installation application from the Internet. If the user chooses to insert the medium, the co-installer should detect the new media notification, silently exit, and allow the medium's AutoRun process to start the device installation application.

    A co-installer can detect the new media by listening for a WM\_DEVICECHANGED/DBT\_DEVICEARRIVAL message with dbch\_devicetype set to DBT\_DEVTYP\_VOLUME and dbcv\_flags set to DBTF\_MEDIA.

    For more information, see [Detecting Media Insertion or Removal](http://go.microsoft.com/fwlink/p/?linkid=161958).

-   A co-installer should never assume that the distribution media is available during installation. For example, a co-installer should never use the %1% DirId to find the media from within the co-installer.

    In Windows Vista and later versions of Windows, the co-installers are invoked after they are copied to the driver store. By this time, the distribution media might are removed, which is why it is important to avoid prompting the user for the medium. For example, suppose that a user performs a [software-first installation](software-first-installation.md), removes the distribution medium, and then plugs in the device. The co-installer is invoked only when the user plugs in the device for the first time.

-   If a co-installer starts Windows Internet Explorer to download the device installation application, it must start it in Protected Mode, which has features that protect users against malicious code.

    For more information about starting Internet Explorer in Protected Mode, see [Understanding and Working in Protected Mode Internet Explorer](http://go.microsoft.com/fwlink/p/?linkid=133163).

For more information about co-installers, see [Writing a Co-installer](writing-a-co-installer.md).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20Guidelines%20for%20Starting%20Device%20Installation%20Applications%20through%20Co-installers%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




