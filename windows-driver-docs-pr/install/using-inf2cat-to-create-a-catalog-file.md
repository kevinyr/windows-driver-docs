---
title: Using Inf2Cat to Create a Catalog File
description: Using Inf2Cat to Create a Catalog File
ms.assetid: 93dea980-eb66-40f0-ac6b-0adaf8376154
---

# Using Inf2Cat to Create a Catalog File


The Inf2Cat tool can be used to create catalog files for any [driver package](driver-packages.md) that has an INF file. For more information about Inf2Cat and its command-line arguments, see [**Inf2Cat**](https://msdn.microsoft.com/library/windows/hardware/ff547089).

**Note**  Prior to the Windows Server 2008 Windows Driver Kit (WDK), the Inf2Cat tool was not part of the WDK tools. However, the tool is installed with the Winqual Submission Tools. To download the Winqual Submission tools, go to the Microsoft [Inf2Cat FAQ](http://go.microsoft.com/fwlink/p/?linkid=79443) website. When the Winqual Submission Tools package is installed, [**Inf2Cat**](https://msdn.microsoft.com/library/windows/hardware/ff547089) is put in the Program Files (x86)\\Microsoft Winqual Submission Tool folder on the system drive.

 

This topic discusses how to create a [catalog file](catalog-files.md) from a driver package's INF file. In this example, the INF file of the *ToastPkg* sample driver package is used. Within the WDK installation directory, this INF file is named *toastpkg.inf* and is located in the *src\\general\\toaster\\toastpkg\\inf* directory.

The name of catalog file that [**Inf2Cat**](https://msdn.microsoft.com/library/windows/hardware/ff547089) produces is specified through the CatalogFile directive. One or more of these directives are declared within the [**INF Version section**](inf-version-section.md) of the INF file. The INF **Version** section of the *toastpkg.inf* file is shown below:

```
[Version]
Signature="$WINDOWS NT$"
Class=TOASTER
ClassGuid={B85B7C50-6A01-11d2-B841-00C04FAD5171}
Provider=%ToastRUs%
DriverVer=09/21/2006,6.0.5736.1
CatalogFile.NTx86  = tostx86.cat
CatalogFile.NTIA64 = tostia64.cat
CatalogFile.NTAMD64 = tstamd64.cat
```

Two things should be noted about this [**INF Version section**](inf-version-section.md):

1.  The [**INF Version section**](inf-version-section.md) declares three different catalog files, one for each Windows version which the driver package supports. When [**Inf2Cat**](https://msdn.microsoft.com/library/windows/hardware/ff547089) is executed, it creates a catalog file for each Windows version that is specified through the **/os** option.

    For example, Inf2Cat creates the catalog file *toastamd64.cat* if the command-line argument /os:Vista\_X64 is used. Similarly, the tool creates the catalog file *toastx86.cat* if the **/os:***Vista\_X86* option is used.

2.  The [**DriverVer directive**](inf-driverver-directive.md) of the INF Version section declares an old time stamp and version.

    Before you use [**Inf2Cat**](https://msdn.microsoft.com/library/windows/hardware/ff547089), you must make sure that the INF file's **DriverVer** directive has a current time stamp and version value. This is needed for the [driver package](driver-packages.md) to install and replace a previously installed version of the package on the test computer.

    You can use the [Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786) tool to update the time stamp and version value in the **DriverVer** directive. For example, to update the **DriverVer** directive in the *toastpkg.inf*, run the following command*:*

    ```
    stampinf -f toastpkg.inf -d 09/01/2008 -v 9.0.9999.0
    ```

The following command line shows how to create a catalog file through the Inf2Cat tool by using the *Toastpkg.inf* file:

```
Inf2cat.exe /driver:src\general\toaster\toastpkg\toastcd\ /os:Vista_x64
```

Where:

-   The **/driver** option specifies the directory which contains one or more INF files. Within this directory, catalog files are created for those INF files that contain one or more CatalogFile directives. For more information about the CatalogFile directive, see [**INF Version sections**](inf-version-section.md).

    In this example, only the *toastpkg*.inf INF file is located within the specified *src\\general\\toaster\\toastpkg\\toastcd* directory.

-   The **/os:***Vista\_x64* option specifies the catalog file is for the 64-bit version of Windows Vista. The Inf2Cat tool will match the name of the catalog file to the requested Windows version. Since the *toastpkg*.inf INF file contains a CatalogFile directive which has the NTAMD64 platform extension, Inf2Cat will create a catalog file that is named *tstamd64.cat.*

    One or more Windows versions may be specified in the **/os:** option. For example, if **/os:***Vista\_x64, Vistax32* is specified, Inf2Cat will create the *tstamd64.cat* and *tstx86.cat* files because of the INF CatalogFile directives in the *toastpkg*.inf INF file.

For more information about the tool's command-line arguments, see [**Inf2Cat**](https://msdn.microsoft.com/library/windows/hardware/ff547089).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20Using%20Inf2Cat%20to%20Create%20a%20Catalog%20File%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




