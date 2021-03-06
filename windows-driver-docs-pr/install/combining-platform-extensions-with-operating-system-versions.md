---
title: Combining Platform Extensions with Operating System Versions
description: Combining Platform Extensions with Operating System Versions
ms.assetid: ef3b7138-b68a-4dba-b011-fcb93e3072a3
---

# Combining Platform Extensions with Operating System Versions


In Windows XP and later versions of Windows, within the [**INF Manufacturer section**](inf-manufacturer-section.md) of an INF file, you can supply [**INF *Models* sections**](inf-models-section.md) that are specific to various versions of the Windows operating system. These version-specific *Models* sections are identified by using the *TargetOSVersion* decoration.

Within the same INF file, different [**INF *Models* sections**](inf-models-section.md) can be specified for different versions of the operating system. The specified versions indicate target operating system versions with which the INF *Models* sections will be used. If no versions are specified, Windows uses a *Models* section without the *TargetOSVersion* decoration for all versions of all operating systems.

### *TargetOSVersion* decoration format

The following example shows the correct format of the *TargetOSVersion* decoration:

**nt**\[*Architecture*\]\[**.**\[*OSMajorVersion*\]\[**.**\[*OSMinorVersion*\]\[**.**\[*ProductType*\]\[**.***SuiteMask*\]\]\]\]

Each field is defined as follows:

<a href="" id="nt"></a>**nt**  
Specifies that the target operating system is NT-based. Windows 2000 and later versions of Windows are all NT-based.

<a href="" id="architecture"></a>*Architecture*  
Identifies the hardware platform. If specified, this must be **x86**, **ia64**, or **amd64**. If not specified, the associated INF *Models* section can be used with any hardware platform.

<a href="" id="osmajorversion"></a>*OSMajorVersion*  
A number that represents the major version number for the operating system. The following table defines the major version for the Windows operating systems.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows version</th>
<th align="left">Major version</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows Server 2008 R2</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 7</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2008</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Vista</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2003</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>5</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="osminorversion"></a>*OSMinorVersion*  
A number that represents the minor version number for the operating system. The following table defines the minor version for the Windows operating systems.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows version</th>
<th align="left">Minor version</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows Server 2008 R2</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 7</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2008</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Vista</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2003</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="producttype"></a>*ProductType*  
A number that represents *one* of the VER\_NT\_*xxxx* flags defined in *Winnt.h*, such as the following:

**0x0000001** (VER\_NT\_WORKSTATION)

**0x0000002** (VER\_NT\_DOMAIN\_CONTROLLER)

**0x0000003** (VER\_NT\_SERVER)

If a product type is specified, the INF file will be used only if the operating system matches the specified product type. If the INF file supports multiple product types for a single operating system version, multiple *TargetOSVersion* entries are required.

*SuiteMask*
A number that represents *a combination of* one or more of the VER\_SUITE\_*xxxx* flags defined in *Winnt.h*. These flags include the following:

**0x00000001** (VER\_SUITE\_SMALLBUSINESS)
**0x00000002** (VER\_SUITE\_ENTERPRISE)
**0x00000004** (VER\_SUITE\_BACKOFFICE)
**0x00000008** (VER\_SUITE\_COMMUNICATIONS)
**0x00000010** (VER\_SUITE\_TERMINAL)
**0x00000020** (VER\_SUITE\_SMALLBUSINESS\_RESTRICTED)
**0x00000040** (VER\_SUITE\_EMBEDDEDNT)
**0x00000080** (VER\_SUITE\_DATACENTER)
**0x00000100** (VER\_SUITE\_SINGLEUSERTS)
**0x00000200** (VER\_SUITE\_PERSONAL)
**0x00000400** (VER\_SUITE\_SERVERAPPLIANCE)
If one or more suite mask values are specified, the INF file will be used only if the operating system matches all the specified product suites. If the INF file supports multiple product suite combinations for a single operating system version, multiple *TargetOSVersion* entries are required.

### <a href="" id="how-setup-processes-targetosversion-decorations"></a>How Windows processes *TargetOSVersion* decorations

When you install a device or driver on a host operating system, Windows follows these steps to process the [**INF *Models* sections**](inf-models-section.md) within an INF file:

1.  If one or more [**INF *Models* sections**](inf-models-section.md) have the *TargetOS* decoration, Windows selects the INF *Models* section that is closest to the attributes for the host operating system.

    For example, if an INF *Models* section has a *TargetOS* decoration of **ntx86.5.1**, Windows selects that section if the host operating system is running Windows XP or later version of Windows on an x86-based system.

    Similarly, if an [**INF *Models* section**](inf-models-section.md) has a *TargetOS* decoration of **nt.6.0**, Windows selects that section if the host operating system is Windows Vista or later version of Windows on any supported hardware platform.

2.  If none of the [**INF *Models* sections**](inf-models-section.md) have a *TargetOS* decoration that matches the host operating system, Windows selects the *Models* section that has either a matching platform extension or no platform extension.

    For example, if an INF *Models* section has a platform extension of **ntx86**, Windows selects that section if the host operating system is Microsoft Windows 2000 or later version of Windows on an x86-based system.

    Similarly, if an [**INF *Models* sections**](inf-models-section.md) has no platform extension, Windows selects that section if the host operating system is Windows 2000 or later version of Windows on any supported hardware platform.

3.  If Windows cannot find a matching [**INF *Models* section**](inf-models-section.md), it will not use the INF file to install the device or driver.

### Sample INF *Models* sections with*TargetOSVersion* decorations

The following topics provide samples of how to decorate platform extensions for target operating systems within an [**INF *Models* section**](inf-models-section.md):

[Sample INF *Models* Sections for One or More Target Operating Systems](sample-inf-models-sections-for-one-or-more-target-operating-system.md)

[Sample INF *Models* Sections for Only One Target Operating System](sample-inf-models-sections-for-only-one-target-operating-system.md)

[Sample INF File for Device Installation on Multiple Versions of Windows](sample-inf-file-for-device-installation-on-multiple-versions-of-windows.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20Combining%20Platform%20Extensions%20with%20Operating%20System%20Versions%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




