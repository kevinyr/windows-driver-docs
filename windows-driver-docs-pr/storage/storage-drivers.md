---
title: Storage Drivers
author: windows-driver-content
description: Storage Drivers
ms.assetid: 5512a8f1-20ad-4b78-a60e-7418ac7f2117
keywords: ["storage drivers WDK"]
---

# Storage Drivers


## <span id="ddk_storage_drivers_kg"></span><span id="DDK_STORAGE_DRIVERS_KG"></span>


This section contains the following information:

[Storage Driver Architecture](storage-driver-architecture.md)

[Storage Drivers and Device Objects](storage-drivers-and-device-objects.md)

[System Header Files for Storage Drivers](system-header-files-for-storage-drivers.md)

[Restrictions on Pageable Code in Storage Drivers](restrictions-on-pageable-code-in-storage-drivers.md)

[Querying for the Write Cache Property](querying-for-the-write-cache-property.md)

[Device Unique Identifiers for Storage Devices (DUIDs)](device-unique-identifiers--duids--for-storage-devices.md)

Subsequent sections contain guidelines for designing the following kinds of Windows kernel-mode storage drivers:

-   An operating system-independent miniport driver for a vendor-specific SCSI HBA (see [SCSI Miniport Drivers](scsi-miniport-drivers.md))

-   A miniport driver for a non-SCSI storage adapter (see [SCSI Miniport Drivers](scsi-miniport-drivers.md))

-   A class driver for a new type of peripheral device (see [Storage Class Drivers](storage-class-drivers.md))

-   An operating system-independent tape miniclass driver for a vendor-specific tape device (see [Tape Drivers](tape-drivers.md))

-   A changer miniclass driver for a vendor-specific medium changer device (see [Changer Drivers](changer-drivers.md))

-   A filter driver for a peripheral device of a type that already has a class driver (see [Storage Filter Drivers](storage-filter-drivers.md))

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[storage\storage]:%20Storage%20Drivers%20%20RELEASE:%20%285/9/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


