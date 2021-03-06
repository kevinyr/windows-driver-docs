---
title: Retrieving Device Relations
description: Retrieving Device Relations
ms.assetid: 2b0ead69-1fda-4024-a7c2-d6350060b5fb
---

# Retrieving Device Relations


In Windows Vista and later versions of Windows, the [unified device property model](unified-device-property-model--windows-vista-and-later-.md) includes [device relations properties](https://msdn.microsoft.com/library/windows/hardware/ff541498). The unified device property model uses [property keys](property-keys.md) to represent these properties.

Windows Server 2003, Windows XP, and Windows 2000 do not support the property keys of the unified property model, nor do they support the corresponding registry entry values that represent these properties. However, you can retrieve the corresponding information by calling Plug and Play (PnP) configuration manager functions. To maintain compatibility with earlier Windows versions, Windows Vista and later versions also support calling PnP configuration manager functions to retrieve device relations properties. However, you should use the property keys of the unified device property model to access the device relation properties.

For information about how to use property keys to access device driver properties, see [Accessing Device Instance Properties (Windows Vista and Later)](accessing-device-instance-properties--windows-vista-and-later-.md).

For information about how to access the device relations properties on Windows Server 2003, Windows XP, and Windows 2000, see the following topics:

[Retrieving Ejection Relations, Removal Relations, and Power Relations, and Bus Relations](#retrieving-ejection-relations--removal-relations--and-power-relations-)

[Retrieving the Parent of a Device Instance](#retrieving-the-parent-of-a-device-inst)

[Retrieving the Children of a Device Instance](#retrieving-the-children-of-a-device-inst)

[Retrieving the Siblings of a Device Instance](#retrieving-the-siblings-of-a-device-inst)

### <a href="" id="retrieving-ejection-relations--removal-relations--and-power-relations-"></a> Retrieving Ejection Relations, Removal Relations, and Power Relations, and Bus Relations

To retrieve device relations information on Windows Server 2003, Windows XP, and Windows 2000, call **CM\_Get\_Device\_ID\_List** and supply the following parameter values:

-   Set *pszFilter* to a pointer to a NULL-terminated string that specifies the device instance identifier for which to retrieve relations information.

-   Set *Buffer* to a pointer to a buffer that receives a list of NULL-terminated device instance identifiers. The list is terminated by an additional NULL character. You can get the required buffer size by calling the **CM\_Get\_Device\_ID\_List\_Size** function.

-   Set *BufferLen* to the size, in characters, of the *Buffer* buffer.

-   Set *ulFlags* to one of the following flags to retrieve the corresponding relations information:
    -   CM\_GETIDLIST\_FILTER\_EJECTIONRELATIONS

        The CM\_GETIDLIST\_FILTER\_EJECTIONRELATIONS flag retrieves [**ejection relations**](https://msdn.microsoft.com/library/windows/hardware/ff551670), which is the same information that is provided by the [**DEVPKEY\_Device\_EjectionRelations**](https://msdn.microsoft.com/library/windows/hardware/ff542482) device property in Windows Vista and later versions.

    -   CM\_GETIDLIST\_FILTER\_REMOVALRELATIONS

        The CM\_GETIDLIST\_FILTER\_REMOVALRELATIONS flag retrieves [**removal relations**](https://msdn.microsoft.com/library/windows/hardware/ff551670), which is the same information that is provided by the [**DEVPKEY\_Device\_RemovalRelations**](https://msdn.microsoft.com/library/windows/hardware/ff542614) device property in Windows Vista and later versions.

    -   CM\_GETIDLIST\_FILTER\_POWERRELATIONS

        The CM\_GETIDLIST\_FILTER\_POWERRELATIONS flag retrieves power relations, which is the same information that is provided by the [**DEVPKEY\_Device\_PowerRelations**](https://msdn.microsoft.com/library/windows/hardware/ff542588) device property in Windows Vista and later versions.

    -   CM\_GETIDLIST\_FILTER\_BUSRELATIONS

        The CM\_GETIDLIST\_FILTER\_BUSRELATIONS flag retrieves [**bus relations**](https://msdn.microsoft.com/library/windows/hardware/ff551670), which is the same information that is provided by the [**DEVPKEY\_Device\_BusRelations**](https://msdn.microsoft.com/library/windows/hardware/ff542368) device property in Windows Vista and later versions.

If the call to **CM\_Get\_Device\_ID\_List** succeeds, **CM\_Get\_Device\_ID\_List** retrieves the requested relations information and returns CR\_SUCCESS. Otherwise, **CM\_Get\_Device\_ID\_List** returns one of the error codes with prefix "CR\_" that are defined in *Cfgmgr32.h*.

### <a href="" id="retrieving-the-parent-of-a-device-inst"></a> Retrieving the Parent of a Device Instance

To retrieve the device instance identifier of a parent device on Windows Server 2003, Windows XP, and Windows 2000, follow these steps:

1.  Call the [**CM\_Get\_Parent**](https://msdn.microsoft.com/library/windows/hardware/ff538610) function to retrieve a device instance handle to the parent device of a device instance.

2.  Call [**CM\_Get\_Device\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff538405) to retrieve the device instance identifier that is associated with the device instance handle to the parent device that was retrieved by the previous call to **CM\_Get\_Parent**.

This information retrieved by using this procedure is the same as that represented by the DEVPKEY\_Device\_Parent property in the unified device property model of Windows Vista and later versions.

### <a href="" id="retrieving-the-children-of-a-device-inst"></a>Retrieving the Children of a Device Instance

To retrieve the device instance identifiers of the child devices of a device instance on Windows Server 2003, Windows XP, and Windows 2000, follow these steps:

1.  Call the [**CM\_Get\_Child**](https://msdn.microsoft.com/library/windows/hardware/ff538074) function to retrieve a device instance handle to the first child device that is associated with a device instance.

2.  Call [**CM\_Get\_Sibling**](https://msdn.microsoft.com/library/windows/hardware/ff538674) as many times as it is necessary to enumerate all the sibling devices of the first child device that was retrieved by the call to **CM\_Get\_Child**.

3.  Call **CM\_Get\_Device\_ID** to retrieve the device instance identifiers that are associated with the device instance handles that were returned by the calls to **CM\_Get\_Child** and **CM\_Get\_Sibling**.

This information retrieved by using this procedure is the same as that represented by the DEVPKEY\_Device\_Children property in the unified device property model of Windows Vista and later versions.

### <a href="" id="retrieving-the-siblings-of-a-device-inst"></a>Retrieving the Siblings of a Device Instance

To retrieve the device instance identifiers of the sibling devices of device instance Abc on Windows Server 2003, Windows XP, and Windows 2000, follow these steps:

1.  Call the [**CM\_Get\_Parent**](https://msdn.microsoft.com/library/windows/hardware/ff538610) function to retrieve a device instance handle to the parent device of device instance *Abc*.

2.  Call the [**CM\_Get\_Child**](https://msdn.microsoft.com/library/windows/hardware/ff538074) function to retrieve a device instance handle to the first child device of the parent device of device instance *Abc*.

3.  Call [**CM\_Get\_Sibling**](https://msdn.microsoft.com/library/windows/hardware/ff538674) as many times as is necessary to enumerate all the sibling devices of the first child device of the parent device. This enumeration will also return a handle to device instance *Abc*.

4.  Call [**CM\_Get\_Device\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff538405) to retrieve the device instance identifiers that are associated with the device instance handles that were returned by the previous calls to **CM\_Get\_Sibling**. Remove the handle to device instance *Abc* from the list of sibling devices of the first child device of the parent device.

The information retrieved by using this procedure is the same as that represented by the DEVPKEY\_Device\_Siblings property in the unified device property model of Windows Vista and later versions. If a **CM\_*Xxx*** function call listed in this section succeeds, the **CM\_*Xxx*** function retrieves the requested information and returns CR\_SUCCESS. Otherwise, the **CM\_*Xxx*** function returns one of the error codes with prefix "CR\_" that are defined in *Cfgmgr32.h*.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20Retrieving%20Device%20Relations%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




