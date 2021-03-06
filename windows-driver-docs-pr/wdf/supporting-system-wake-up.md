---
title: Supporting System Wake-Up
author: windows-driver-content
description: Supporting System Wake-Up
ms.assetid: 519dcd1a-9975-48b1-a032-04348b903ac5
keywords: ["system wake-up WDK KMDF", "power management WDK KMDF , wake-up capabilities", "wake-up capabilities WDK KMDF", "sleep power management WDK KMDF", "low-power states WDK KMDF", "Power Management Event WDK KMDF", "PME WDK KMDF", "Power Management Capabilities WDK KMDF", "PMC WDK KMDF"]
---

# Supporting System Wake-Up


While the system is in a low-power state, some devices can detect an external event, such as an incoming network packet, and then wake the system. For example, if a PCI device has a system wakeup capability, as indicated in the device's Power Management Capabilities (PMC) register, it wakes the system by raising the Power Management Event (PME) signal on the PCI bus.

If your device can wake the system from a system-wide low-power state, the [*EvtDriverDeviceAdd*](https://msdn.microsoft.com/library/windows/hardware/ff541693) callback function in the [power policy owner](power-policy-ownership.md) must perform the following two steps:

1.  Call [**WdfDeviceAssignSxWakeSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545909) to specify:

    -   The low-power state that the device will enter
    -   Whether users can control the device's idle settings
    -   Whether the device's wake capability is enabled or disabled

    For more information about these settings, see the [**WDF\_DEVICE\_POWER\_POLICY\_WAKE\_SETTINGS**](https://msdn.microsoft.com/library/windows/hardware/ff551277) structure.

2.  Call [**WdfDeviceInitSetPowerPolicyEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff546774) to register the following event callback functions, if you need them for your device:
    -   [*EvtDeviceArmWakeFromSx*](https://msdn.microsoft.com/library/windows/hardware/ff540844) or [*EvtDeviceArmWakeFromSxWithReason*](https://msdn.microsoft.com/library/windows/hardware/ff540846), which enable the device hardware to respond to an external wake-up event.
    -   [*EvtDeviceDisarmWakeFromSx*](https://msdn.microsoft.com/library/windows/hardware/ff540862), which disables the device's ability to respond to an external wake-up event.
    -   [*EvtDeviceWakeFromSxTriggered*](https://msdn.microsoft.com/library/windows/hardware/ff540923), which informs the driver that the bus detected a wake signal.

Bus drivers also participate in waking up the system. The driver for the device's bus typically provides [*EvtDeviceEnableWakeAtBus*](https://msdn.microsoft.com/library/windows/hardware/ff540866) and [*EvtDeviceDisableWakeAtBus*](https://msdn.microsoft.com/library/windows/hardware/ff540858) callback functions. These functions do whatever is necessary on the bus adapter to enable and disable a device's ability to wake from a low-power state.

When a bus driver determines that a device has triggered a wake signal, it must call [**WdfDeviceIndicateWakeStatus**](https://msdn.microsoft.com/library/windows/hardware/ff546025) to inform the framework that the device's power should be restored. The framework then passes this information to the rest of the drivers in the driver stack.

For information about registry entries that control a device's wake capabilities, see [User Control of Device Idle and Wake Behavior](user-control-of-device-idle-and-wake-behavior.md).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bwdf\wdf%5D:%20Supporting%20System%20Wake-Up%20%20RELEASE:%20%284/5/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




