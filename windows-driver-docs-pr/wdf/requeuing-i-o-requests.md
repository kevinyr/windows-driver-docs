---
title: Requeuing I/O Requests
author: windows-driver-content
description: Requeuing I/O Requests
ms.assetid: b509959c-b2ab-4f04-9c08-5c5e90726b73
keywords: ["I/O requests WDK KMDF , requeuing", "requeuing I/O requests WDK KMDF", "request processing WDK KMDF , requeuing I/O requests"]
---

# Requeuing I/O Requests


## <a href="" id="ddk-requeuing-i-o-requests-df"></a>


Drivers can requeue I/O requests that they obtain from an I/O queue. A driver can requeue a I/O request to another I/O queue that the driver has created for the same device. In addition, a [bus driver](https://msdn.microsoft.com/library/windows/hardware/ff540704) can requeue an I/O request from a child device's I/O queue to a parent device's I/O queue.

### Requeuing an I/O Request to a Different I/O Queue for a Device

After a driver's request handlers receives an I/O request from a driver's I/O queue, the driver can call [**WdfRequestForwardToIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549958) to requeue the request to another queue.

For example, if you want your driver to allocate resources to a request before processing the request, the driver's [*EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757) callback function could receive all requests, store resource information in each request's context memory, and then call [**WdfRequestForwardToIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549958) to requeue each request to an additional queue.

If your driver calls [**WdfRequestForwardToIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549958) to requeue an I/O request that the driver obtained from an I/O queue that is using the sequential [dispatching method](dispatching-methods-for-i-o-requests.md), the framework will deliver the next I/O request from the sequential queue to the driver without waiting for the requeued request to complete.

If your driver is using the manual dispatching method, it can call the [**WdfRequestRequeue**](https://msdn.microsoft.com/library/windows/hardware/ff550012) method to return an I/O request to the head of the I/O queue from which the driver obtained it. After calling **WdfRequestRequeue**, the driver's next call to [**WdfIoQueueRetrieveNextRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548462) retrieves the requeued request.

### Requeuing an I/O Request to a Parent Device's I/O Queue

A function driver for a parent device can act as a [bus driver](https://msdn.microsoft.com/library/windows/hardware/ff540704) that [enumerates](enumerating-the-devices-on-a-bus.md) the child devices of the parent device and creates [physical device objects](wdm-concepts-for-kmdf-drivers.md#device-stacks) (PDOs) for the child devices. Such drivers can sometimes receive I/O requests for a child device that the parent device must handle.

For example, a protocol bus (such as USB) typically controls the hardware resources that are assigned to each connected device. Therefore, the function driver for the parent bus typically handles I/O operations for each child device. When the I/O manager sends an I/O request to the [device stack](wdm-concepts-for-kmdf-drivers.md#device-stacks) of one of the child devices, the function driver for the bus receives the I/O request in one of the child device's I/O queues, because that driver created the child device's PDO. Before the driver can process the I/O request in the context of the parent bus device, it must requeue the I/O request from the child device's I/O queue to an I/O queue that belongs to the parent device.

However, drivers cannot call [**WdfRequestForwardToIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549958) to move requests from a child's queue to a parent's queue. Because the I/O manager creates separate device stacks for the parent and child devices, the underlying WDM device object must first be changed from one that represents the child device to one that represents the parent.

Prior to version 1.9 of KMDF, drivers could send I/O requests from a child device to its parent only by creating [remote I/O targets](general-i-o-targets.md), increasing the size of the child device's device stack, and specifying the correct WDM device object.

Beginning with KMDF version 1.9, a driver can call [**WdfPdoInitAllowForwardingRequestToParent**](https://msdn.microsoft.com/library/windows/hardware/ff548789) before it creates a child device and then call [**WdfRequestForwardToParentDeviceIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549959) to requeue a request from the child's I/O queue to a parent queue. If a driver uses**WdfPdoInitAllowForwardingRequestToParent** and **WdfRequestForwardToParentDeviceIoQueue**, the framework increases the child's device stack size and assigns the correct WDM device object to the I/O request.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bwdf\wdf%5D:%20Requeuing%20I/O%20Requests%20%20RELEASE:%20%284/5/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




