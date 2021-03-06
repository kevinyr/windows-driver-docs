---
title: IPM Hard Disk Drive Idle Timeout
author: windows-driver-content
description: IPM Hard Disk Drive Idle Timeout
ms.assetid: 1dcc261a-803c-4c0e-a68e-29b00f46cd32
---

# IPM Hard Disk Drive Idle Timeout


Although the hard disk drive (HDD) is not the primary power consumer in the typical mobile PC, power savings can be realized by spinning down the HDD media. The HDD idle timeout allows Windows to automatically spin down the HDD media after a period of disk read and write inactivity.

The power savings that are realized when the HDD media is spun down varies by the make and model of the HDD. We encourage system manufacturers to work with HDD vendors to determine the optimal HDD idle timeout value for specific devices.

By default, Windows Vista specifies moderately long HDD idle timeout values. System manufacturers should consider specifying shorter values when trying to achieve aggressive battery conservation on mobile PCs. The following table summarizes details of the HDD idle settings.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Detail</strong></p></td>
<td align="left"><p><strong>Description</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>Friendly name</p></td>
<td align="left"><p>Turn off hard disk after</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Description</p></td>
<td align="left"><p>Specifies how long the hard drive is inactive before the disk turns off</p></td>
</tr>
<tr class="even">
<td align="left"><p>PowerCfg Alias</p></td>
<td align="left"><p>DISKIDLE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Group policy path</p></td>
<td align="left"><p>Administrative Templates\System\Power Management\Hard Disk Settings\Turn Off the Hard Disk</p></td>
</tr>
<tr class="even">
<td align="left"><p>GUID</p></td>
<td align="left"><p>6738e2c4-e8a5-4a42-b16a-e040e769756e</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Defined in</p></td>
<td align="left"><p>Ntpoapi.h</p></td>
</tr>
<tr class="even">
<td align="left"><p>Balanced defaults</p></td>
<td align="left"><p>60 minutes (AC) 30 minutes (DC)</p></td>
</tr>
</tbody>
</table>

 

For more information see [Mobile Battery Life Solutions - A Guide for Mobile Platform Professionals.](http://go.microsoft.com/fwlink/p/?linkid=144534)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[storage\storage]:%20IPM%20Hard%20Disk%20Drive%20Idle%20Timeout%20%20RELEASE:%20%285/9/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


