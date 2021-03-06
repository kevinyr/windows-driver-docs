---
title: Using the Registry in UMDF 1.x Drivers
author: windows-driver-content
description: Using the Registry in UMDF 1.x Drivers
ms.assetid: 653f996a-9fc8-461f-b284-a5d6795259d6
keywords: ["registry WDK UMDF", "property store objects WDK UMDF", "UMDF drivers WDK UMDF , registry", "user-mode drivers WDK UMDF , registry", "UMDF WDK , registry", "User-Mode Driver Framework WDK , registry", "keys WDK UMDF"]
---

# Using the Registry in UMDF 1.x Drivers


\[This topic applies to UMDF 1.*x*.\]

UMDF-based drivers can read and write values in the registry by using interfaces of the property store object.

UMDF-based drivers can access four types of registry keys. Drivers can create, read, and write subkeys and values under these keys. The following types of registry keys are available to UMDF-based drivers:

-   Hardware keys

    The PnP manager creates a hardware key, or *device key*, for each device, in which it stores the device's unique identification information.

    Your driver can retrieve and modify some of the property values under the hardware key. The location of the stored values depends on the method that you use to access them.

    Property values that were created using PropertyStore methods are stored in the **\\Device Parameters** subkey, under the hardware key. To access these properties, your driver calls one of the following methods to obtain a property store interface.

    <a href="" id="iwdfdevice--retrievedevicepropertystore"></a>[**IWDFDevice::RetrieveDevicePropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff558842)  
    Obtains a pointer to an [**IWDFNamedPropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff560164) interface.

    <a href="" id="iwdfdeviceinitialize--retrievedevicepropertystore"></a>[**IWDFDeviceInitialize::RetrieveDevicePropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff556982)  
    Obtains a pointer to an [**IWDFNamedPropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff560164) interface.

    <a href="" id="iwdfpropertystorefactory--retrievedevicepropertystore"></a>[**IWDFPropertyStoreFactory::RetrieveDevicePropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff560228)  
    Obtains a pointer to an [**IWDFNamedPropertyStore2**](https://msdn.microsoft.com/library/windows/hardware/ff560168) interface. You can use the *SubkeyPath* parameter to specify values under a driver-created subkey, such as **\\Device Parameters\\***DriverServiceName\\subkey*.

    Drivers have read-only access to values within the **\\Device Parameters** subkey, and cannot access **\\Device Parameters\\WDF** or **\\Device Parameters\\WUDF**.

    Property values that were created using the Unified Device Property model are stored in the **\\Properties** subkey, under the hardware key.

    To access these properties, your driver calls [**IWDFUnifiedPropertyStoreFactory::RetrieveUnifiedDevicePropertyStore**](https://msdn.microsoft.com/library/windows/hardware/hh451406) to obtain a property store interface. Then the driver can use the [**IWDFUnifiedPropertyStore**](https://msdn.microsoft.com/library/windows/hardware/hh451399) interface to modify and retrieve current settings of device properties.

-   Software keys

    A driver's software key is also called its *driver key* because the registry contains a software key for each driver. The registry contains a list of all of the device classes, and each driver's software key resides under its device class entry. The system stores information about each driver under its software key.

    Your driver can call [**IWDFPropertyStoreFactory::RetrieveDevicePropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff560228) to obtain read or write access to values under its software key. The driver can read and write driver-specific information that is not associated with specific devices.

-   Device interface keys

    The registry contains keys for all of the [device interface classes](https://msdn.microsoft.com/library/windows/hardware/ff541339) that drivers have created. Under each of these keys is an entry for each instance of the device interface class that a driver has registered.

    If your driver has registered an instance of a device interface class, it can read and write values under the registry's entry for that instance by calling [**IWDFPropertyStoreFactory::RetrieveDevicePropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff560228). The driver can read and write instance-specific information about the device interface.

-   The **DEVICEMAP** key

    The registry contains a **HKEY\_LOCAL\_MACHINE\\HARDWARE\\DEVICEMAP** key that some drivers for older technologies, such as serial and parallel ports, use. If your driver supports a technology that uses the **DEVICEMAP** key, the driver can access subkeys and values under the key by calling [**IWDFPropertyStoreFactory::RetrieveDevicePropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff560228).

After a driver has called one of the **RetrieveDevicePropertyStore** methods to open a registry subkey, the driver can use methods exposed by [**IWDFNamedPropertyStore**](https://msdn.microsoft.com/library/windows/hardware/ff560164), [**IWDFNamedPropertyStore2**](https://msdn.microsoft.com/library/windows/hardware/ff560168), or [**IWDFUnifiedPropertyStore**](https://msdn.microsoft.com/library/windows/hardware/hh451399) to create, read, and write values under a subkey. The **IWDFNamedPropertyStore2** interface also enables drivers to delete values.

For more information about registry keys for drivers, see [Overview of Registry Trees and Keys](https://msdn.microsoft.com/library/windows/hardware/ff549538).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bwdf\wdf%5D:%20Using%20the%20Registry%20in%20UMDF%201.x%20Drivers%20%20RELEASE:%20%284/5/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




