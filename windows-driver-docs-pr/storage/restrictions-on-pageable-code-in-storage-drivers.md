---
title: Restrictions on Pageable Code in Storage Drivers
author: windows-driver-content
description: Restrictions on Pageable Code in Storage Drivers
ms.assetid: 1958f22f-5563-41e9-9c3f-dec8a4ac80c0
keywords: ["storage drivers WDK , pageable code restrictions", "pageable code restrictions WDK storage", "deadlocks WDK storage", "paging path WDK storage"]
---

# Restrictions on Pageable Code in Storage Drivers


## <span id="ddk_restrictions_on_pageable_code_in_storage_drivers_kg"></span><span id="DDK_RESTRICTIONS_ON_PAGEABLE_CODE_IN_STORAGE_DRIVERS_KG"></span>


To prevent deadlock, no part of a storage driver that is used to service read or write requests should have pageable code, nor should it ever attempt to access pageable memory. This is because the driver's [**DispatchRead**](https://msdn.microsoft.com/library/windows/hardware/ff543376) and [**DispatchWrite**](https://msdn.microsoft.com/library/windows/hardware/ff544034) routines can be called at IRQL &gt; PASSIVE\_LEVEL, and the in-paging I/O that services a page fault takes place at IRQL = APC\_LEVEL.

Similar rules apply to a storage driver's device control dispatch routine, [**DispatchDeviceControl**](https://msdn.microsoft.com/library/windows/hardware/ff543287), with certain qualifications. A storage driver's device control dispatch routine must not contain pageable code or access pageable memory. The dispatch routine must be able to receive IOCTL requests that are intended for other drivers at arbitrary IRQLs and pass them down the driver stack. Drivers *must* pass all unhandled IOCTL requests down the stack without altering the IRQL or the context of the request.

However, Microsoft requires that all *storage* IOCTL requests be submitted at PASSIVE\_LEVEL, so although the dispatch routine is not itself pageable, it can call pageable subroutines to handle storage IOCTL requests. These subroutines can also access pageable memory.

Routines such as [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113), [**Reinitialize**](https://msdn.microsoft.com/library/windows/hardware/ff561022), and [**Unload**](https://msdn.microsoft.com/library/windows/hardware/ff564886), that do no I/O and run at IRQL = PASSIVE\_LEVEL can also have pageable code.

Special considerations apply to drivers that manage storage devices in the paging path. A driver is in the "paging path" if it participates in I/O operations on the paging file. When a storage driver is in the paging path, its [**DispatchPower**](https://msdn.microsoft.com/library/windows/hardware/ff543354) routine for IRP\_MJ\_POWER requests must not be pageable.

By default, the code for kernel-mode drivers is not pageable, nor is the global memory used by kernel-mode drivers pageable. For information about how to make code pageable, see [Making Driver Code or Data Pageable](https://msdn.microsoft.com/library/windows/hardware/ff554349).

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[storage\storage]:%20Restrictions%20on%20Pageable%20Code%20in%20Storage%20Drivers%20%20RELEASE:%20%285/9/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


