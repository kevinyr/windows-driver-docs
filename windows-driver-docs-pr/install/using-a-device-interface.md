---
title: Using a Device Interface
description: Using a Device Interface
ms.assetid: a41f9ae2-6128-43e2-a6b5-4d0bd45371bd
keywords: ["interface classes WDK device installations", "device interface classes WDK device installations"]
---

# Using a Device Interface


## <a href="" id="ddk-using-a-device-interface-dg"></a>


Device interfaces are available to both kernel-mode components and user-mode applications. User-mode code can use **SetupDi***Xxx* functions to find out about registered, enabled device interfaces. See [SetupDi Device Interface Functions](using-device-installation-functions.md#ddk-setupdi-device-interface-functions-dg) for more information.

Before a kernel-mode component can use a specific device or file object, it must do the following:

1.  Determine whether the required device interface class is registered and enabled.

    A driver can register with the PnP manager to be notified when an instance of a device interface is enabled or disabled. To register, the component calls [**IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526). This routine stores the address of a driver-supplied callback, which is called whenever an instance of a device interface instance is enabled or disabled, for a specified device class. The callback routines receive the [**DEVICE\_INTERFACE\_CHANGE\_NOTIFICATION**](https://msdn.microsoft.com/library/windows/hardware/ff543134) structure, which contains a Unicode string representing the interface instance's symbolic link. See [Using PnP Device Interface Change Notification](https://msdn.microsoft.com/library/windows/hardware/ff565474) for more information.

    A driver or other kernel-mode component can also call [**IoGetDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff549186) to get a list of all registered, enabled device interface instances for a specific device interface class. The returned list contains pointers to the Unicode symbolic link strings that identify the device interface instances.

2.  Get a pointer to a device or file object that corresponds to an instance of the interface.

    To access a specific device object, the driver must call [**IoGetDeviceObjectPointer**](https://msdn.microsoft.com/library/windows/hardware/ff549198), passing the Unicode string for the required interface in the *ObjectName* parameter. To access a file object, the driver must call [**InitializeObjectAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff547804), passing the Unicode string in the *ObjectName* parameter, and then pass the successfully initialized attribute structure in a call to [**ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20Using%20a%20Device%20Interface%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




