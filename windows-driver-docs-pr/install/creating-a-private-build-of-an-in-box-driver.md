---
title: Creating a Private Build of an Inbox Driver
description: Creating a Private Build of an Inbox Driver
ms.assetid: aed3c175-3e95-4bfb-a514-a663dd9e3f57
---

# Creating a Private Build of an Inbox Driver


When you build a private version of the inbox driver, and [Windows is configured to rank driver signatures equally](configuring-windows-to-rank-driver-signatures-equally.md), you must ensure that the private build outranks the Microsoft-signed version. The simplest way to ensure this is to update the value of the [**INF DriverVer directive**](inf-driverver-directive.md) in the [driver package's](driver-packages.md) INF file. The new value must specify a date and version that is later than the value of the **DriverVer** directive in the package's INF file that is installed on the target system.

You can automate the process for building a private version of an inbox driver that outranks the Microsoft-signed version by following these steps:

1.  Modify the makefile to generate a new INF file for the [driver package](driver-packages.md). For example, add the following line to the *Makefile*:

    ```
    $(O)\sample.inf
    ```

2.  Add directives to the *Makefile* that will generate a new INF file and execute the [Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786) tool to time stamp the INF file. For example, the following code example shows how you can create and time stamp an INF file that is named *Sample.inf*:

    ```
    $(O)\ sample.inf: $(_INX)\ sample.inx $(_LNG)\ sample.txt
        $(C_PREPROCESSOR_NAME) $(PREFLAGS) $(_LNG)\$(@B).txt > $(O)\$(@B).txt1
        copy /b $(_INX)\$(@B).inx+$(O)\$(@B).txt1 $@
        @del $(O)\$(@B).txt1
        stampinf -f sample.inf -d * -v * -c MyCatalogFile.cat
        $(TSBINPLACE_CMD)
    ```

    The following [Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786) command-line parameters are used in this example:

    -   The -d \* parameter uses the current date as part of the DriverVer directive in the INF file.
    -   The **-v \*** parameter uses the current time for the version number. If the STAMPINF\_VERSION environment variable is set, Stampinf uses the version number value that is specified by this environment variable.
    -   The -**c** parameter specifies the name of the [catalog file](catalog-files.md) for the [driver package](driver-packages.md). This value is written to the **CatalogFile** directive of the [**INF Version section**](inf-version-section.md) of the generated IF file.

    **Note**  If you set the environment variable PRIVATE\_DRIVER\_PACKAGE, Stampinf uses the current date and version for the INF **DriverVer** directive. By setting this environment variable, you do not have to use the **-d** or **-v** parameters in your *Makefile*.

     

Once the driver is built, you must sign the [driver package](driver-packages.md) and must use the same [catalog file](catalog-files.md) that was specified in the **-c** parameter of [Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786) within your *Makefile*. To sign the driver package, follow the steps that are outlined in [Signing Drivers During Development and Test (Windows Vista and Later)](signing-drivers-during-development-and-test--windows-vista-and-later-.md).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20Creating%20a%20Private%20Build%20of%20an%20Inbox%20Driver%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




