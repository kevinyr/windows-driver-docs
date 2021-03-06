---
title: GpioClx I/O and Interrupt Interfaces
author: windows-driver-content
description: Typically, the clients of a GPIO controller are drivers for peripheral devices that connect to GPIO pins.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: F75E9B21-9DA4-4DD9-BB44-59E19EDFC099
---

# GpioClx I/O and Interrupt Interfaces


Typically, the clients of a GPIO controller are drivers for peripheral devices that connect to GPIO pins. These drivers use GPIO pins as low-bandwidth data channels, device-select outputs, and interrupt-request inputs. Peripheral device drivers open logical connections to GPIO pins that are configured as data inputs or outputs. They use these connections to send I/O requests to these pins. In addition, peripheral device drivers can logically connect their interrupt service routines to GPIO pins that are configured as interrupt request inputs.

GPIO pins are system-managed hardware resources. Before a peripheral device driver starts its device, the Plug and Play (PnP) manager assigns to this driver a list of hardware resources. This list of hardware resources might include the following:

-   A GPIO I/O resource. This resource is a set of one or more GPIO pins that are configured as data inputs or data outputs. GPIO I/O resources are a new Windows resource type starting with Windows 8.
-   An interrupt. This interrupt resource might be implemented as a GPIO pin that is configured as an interrupt input, but it might be implemented instead by a programmable interrupt controller or as a dedicated interrupt pin on a processor package. The hardware abstraction layer (HAL) interrupt abstraction hides these implementation details, which client drivers can safely ignore.

Before a peripheral device driver can use a set of GPIO pins as data inputs or outputs, the driver must open a logical connection to these pins. For example, a [kernel-mode driver interface](https://msdn.microsoft.com/library/windows/hardware/ff544296) (KMDF) driver obtains a WDFIOTARGET handle to identify the connection. The driver uses this handle to send I/O requests to the pins. Specifically, client drivers send [**IOCTL\_GPIO\_WRITE\_PINS**](https://msdn.microsoft.com/library/windows/hardware/hh406487) and [**IOCTL\_GPIO\_READ\_PINS**](https://msdn.microsoft.com/library/windows/hardware/hh406483) I/O control requests to write data to output pins and read data from input pins. For code examples that show how to connect to a set of GPIO I/O pins, see the following topics:

[Connecting a KMDF Driver to GPIO I/O Pins](https://msdn.microsoft.com/library/windows/hardware/hh406474)
[Connecting a UMDF Driver to GPIO I/O Pins](https://msdn.microsoft.com/library/windows/hardware/hh698244)
To use an interrupt resource to receive interrupts, a peripheral device driver must logically connect an interrupt service routine (ISR) to the interrupt. For example, a kernel-mode driver can make this connection by calling the [**WdfInterruptCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547345) method or the [**IoConnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff548378) routine. After being connected, the driver's ISR runs when the peripheral device signals an interrupt request to the GPIO pin or interrupt controller input. For more information about interrupts, see [Creating an Interrupt Object](https://msdn.microsoft.com/library/windows/hardware/ff540757).

The GPIO framework extension (GpioClx) manages both I/O connections and interrupt connections for the peripheral device drivers that are its clients. The PnP manager might assign different groups of GPIO pins on a GPIO controller device to different client drivers. Some of these pins are configured as data inputs or outputs, and some are configured as interrupt request inputs.

When client drivers receive interrupt requests or send I/O requests to GPIO pins, GpioClx calls event callback functions that are implemented by the GPIO controller driver. These callbacks access the hardware registers in the GPIO controller device. Through these function calls, GpioClx reads data inputs, writes to data outputs, and manages interrupt requests (by querying, enabling, masking, clearing, and so on, GPIO pins that are configured as interrupt inputs).

GpioClx does all the processing that is required to manage I/O and interrupt connections that are opened by clients. The GPIO controller driver—by delegating the management of these connections to GpioClx—is responsible only for the relatively simple task of accessing the hardware registers in the GPIO controller device. The GPIO controller driver does not need to know the client driver for which a particular access is made.

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bgpio\parports%5D:%20GpioClx%20I/O%20and%20Interrupt%20Interfaces%20%20RELEASE:%20%286/3/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


