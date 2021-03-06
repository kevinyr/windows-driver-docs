---
title: Initializing the Battery Class Device
description: Initializing the Battery Class Device
ms.assetid: d385533e-790a-47b3-a3d2-d620cbd40a4d
keywords: ["battery class drivers WDK , device initializations", "battery miniclass drivers WDK , registering", "registering battery devices", "initializing battery devices"]
---

# Initializing the Battery Class Device


## <span id="ddk_initializing_the_battery_class_device_dg"></span><span id="DDK_INITIALIZING_THE_BATTERY_CLASS_DEVICE_DG"></span>


The [*AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521) routine must initialize the battery class device and register the miniclass driver with the class driver. To do so, the miniclass driver calls the [**BatteryClassInitializeDevice**](https://msdn.microsoft.com/library/windows/hardware/ff536266) routine. This call registers the miniclass driver with the class driver, so that the two drivers can use each other's support routines. This call also registers the battery device with the system so that it can be seen by the composite battery and the power meter.

**BatteryClassInitializeDevice** requires a pointer to a [**BATTERY\_MINIPORT\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff536287) structure that contains the following information:

-   In **MajorVersion** and **MinorVersion**, the major and minor version numbers of the class driver that this miniclass driver supports.

    The version numbers are defined in Batclass.h as BATTERY\_CLASS\_MAJOR\_VERSION and BATTERY\_CLASS\_MINOR\_VERSION, respectively.

-   In **QueryTag**, the entry point of the miniclass driver's [*BatteryMiniQueryTag*](https://msdn.microsoft.com/library/windows/hardware/ff536275) routine.

-   In **QueryInformation**, the entry point of the miniclass driver's [*BatteryMiniQueryInformation*](https://msdn.microsoft.com/library/windows/hardware/ff536273) routine.

-   In **SetInformation**, the entry point of the miniclass driver's [*BatteryMiniSetInformation*](https://msdn.microsoft.com/library/windows/hardware/ff536276) routine.

-   In **SetStatusNotify**, the entry point of the miniclass driver's [*BatteryMiniSetStatusNotify*](https://msdn.microsoft.com/library/windows/hardware/ff536277) routine.

-   In **DisableStatusNotify**, the entry point of the miniclass driver's [*BatteryMiniDisableStatusNotify*](https://msdn.microsoft.com/library/windows/hardware/ff536272) routine.

-   In **Context**, a pointer to the miniclass driver's context information.

    The context information is typically a pointer to the FDO device extension, which is passed back to the miniclass driver each time the class driver calls a [BatteryMini*Xxx*](https://msdn.microsoft.com/library/windows/hardware/ff536286) routine.

-   In **Pdo**, a pointer to the PDO for the device.

-   In **DeviceName**, a NULL parameter; PnP devices should not have names.

After setting up this structure, the miniclass driver attaches itself to the battery class driver by calling **BatteryClassInitializeDevice**, and passing a pointer to the BATTERY\_MINIPORT\_INFO structure. In return, it receives a handle to be used in subsequent calls to battery class driver support routines. The miniclass driver should store the returned class handle in nonpaged memory.

After calling **BatteryClassInitializeDevice**, the [*AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521) routine might also need to initialize other device-specific data.

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[battery\battery]:%20Initializing%20the%20Battery%20Class%20Device%20%20RELEASE:%20%286/7/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


