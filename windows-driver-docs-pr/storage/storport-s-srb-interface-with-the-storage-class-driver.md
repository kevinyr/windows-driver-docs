---
title: Storport's SRB Interface with the Storage Class Driver
author: windows-driver-content
description: Storport's SRB Interface with the Storage Class Driver
ms.assetid: c7e55516-0ba9-48bc-9b68-e6344552f070
---

# Storport's SRB Interface with the Storage Class Driver


Storage class drivers and other higher-level components communicate with the Storport driver by building SCSI Request Blocks (SRBs). An SRB contains a SCSI command descriptor block (CDB) and a pointer to the data buffer that is to be used to transfer data to or from the device (if any). It may contain a pointer to a sense buffer that is used to hold SCSI sense data in the event the SCSI command fails with Check Condition status. For more information about SRBs, see [**SCSI\_REQUEST\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff565393). Storage class drivers pass the SRBs that they create to Storport in an IRP with the **MajorFunction** member set to IRP\_MJ\_SCSI. For a description of the steps that a storage class driver must take to build an SRB before passing it to a port driver, see [Storage Class Driver's BuildRequest Routine](storage-class-driver-s-buildrequest-routine.md).

Before forwarding an SRB down the stack, Storport sets certain values in the SRB, such as the path, the target number, and the logical unit number of the target device.

Unlike other port drivers, such as the system-supplied port drivers for the IDE/ATAPI and IEEE 1394 buses, Storport does not have to translate the command descriptor block (CDB) in the SRBs that it receives into a different format before forwarding it to the underlying adapter. Storport simply adds some target-specific information to the SRB and passes it to the miniport driver with the CDB unaltered. Therefore, Storport simply passes SRBs that contain CDBs down the stack.

For this reason, most aspects of the SRB interface between the storage class driver and Storport are covered in the general documentation for storage class and storage miniport drivers and their accompanying reference materials. For a list of sections related to the SRB interface between the storage class driver and the Storport-miniport driver pair, see [Storport's Interface with Storport Miniport Drivers](storport-s-interface-with-storport-miniport-drivers.md).

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[storage\storage]:%20Storport's%20SRB%20Interface%20with%20the%20Storage%20Class%20Driver%20%20RELEASE:%20%285/9/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


