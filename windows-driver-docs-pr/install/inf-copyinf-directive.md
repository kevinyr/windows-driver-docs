---
title: INF CopyINF Directive
description: A CopyINF directive causes specified INF files to be copied to the target system. The CopyINF directive is supported in Windows XP and later versions of Windows.
ms.assetid: 289822a8-69c3-43a3-ab07-ee02a7473db8
keywords: ["INF CopyINF Directive Device and Driver Installation"]
topic_type:
- apiref
api_name:
- INF CopyINF Directive
api_type:
- NA
---

# INF CopyINF Directive


A **CopyINF** directive causes specified INF files to be copied to the target system. The **CopyINF** directive is supported in Windows XP and later versions of Windows.

``` syntax
[DDInstall]
  
CopyINF=filename1.inf[,filename2.inf]...
```

Remarks
-------

System support for the **CopyINF** directive is available in Microsoft Windows XP and later versions of Windows.

This directive is typically used when installing multifunction devices. If the installation of a multifunction device requires multiple INF files (for multiple functions that belong to multiple setup classes), using this directive ensures that Windows will find the INF files when it installs the functions. Use the following rules:

-   If the functions that are supplied by a multifunction device are enumerated as children of a parent device (such as an IEEE 1284.4 device), the INF file for the parent device should have a **CopyINF** directive to copy the INF files for the device's individual functions.

-   If all the functions that are supplied by a multifunction device (such as a PCI card) are enumerated as peers of one another, the INF file for each function should have a **CopyINF** directive to copy the INF files for all peer functions.

If you follow these rules, Windows can install drivers for each function without prompting the user for an installation disk for each function.

The following points apply to the **CopyINF** directive:

-   Before Windows Vista, Windows copies the specified INF files as part of the default processing for [**DIF\_INSTALLDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff543692) (see [**SetupDiInstallDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552039)) after the device is installed successfully.

    Windows copies the specified INF files into a system directory path that it will search during device installations.

-   The INF files that are specified in the **CopyINF** directive must reside in the same directory as the INF file that contains the **CopyINF** directive.
-   You must include all INF files on each disk of a multidisk installation.

Starting with Windows Vista, the following points also apply to the **CopyINF** directive:

-   The **CopyINF** directive causes the complete [driver package](driver-packages.md) that is referenced by the specified INF file to be copied into the [driver store](driver-store.md). This is required in order to support the deployment of multifunction driver packages, because the original source media might not be available when the device is actually installed. If the driver package that is referenced by the specified INF file already exists in the driver store, the INF file specified in the **CopyINF** directive is ignored.

-   The **CopyINF** directive is processed during driver store import instead of during device installation. This means that a call to [SetupCopyOEMInf](http://go.microsoft.com/fwlink/p/?linkid=194252) on Windows Vista and later versions of Windows causes all the **CopyINF** directives in the specified INF file to be processed at that time. This occurs recursively for each **CopyINF** directive that is contained within the specified INF file until all referenced driver packages are copied into the driver store.

Starting with Windows 10, version 1511, under certain circumstances (for example, running Windows Update or some calls to [**DiInstallDevice**](https://msdn.microsoft.com/library/windows/hardware/ff544710)), INFs copied with **CopyINF** will also be installed on applicable devices.

For more information about how to copy INF files, see [Copying INFs](copying-inf-files.md).

Examples
--------

```
[MyMfDevice.NTx86]
CopyINF = Sound.INF
```

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20INF%20CopyINF%20Directive%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




