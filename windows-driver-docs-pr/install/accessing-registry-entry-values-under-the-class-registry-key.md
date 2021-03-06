---
title: Accessing Registry Entry Values Under the Class Registry Key
description: Accessing Registry Entry Values Under the Class Registry Key
ms.assetid: 771b5751-db9f-43fa-90d1-1c43918a3a80
---

# Accessing Registry Entry Values Under the Class Registry Key


In Windows Vista and later versions of Windows, the [unified device property model](unified-device-property-model--windows-vista-and-later-.md) includes [device setup class properties](accessing-device-setup-class-properties.md) that do not have corresponding SPCRP\_*Xxx* identifiers. These properties characterize a device setup class. The unified device property model uses [property keys](property-keys.md) to represent these properties.

Windows Server 2003, Windows XP, and Windows 2000 also support most of these device setup class properties. However, these earlier versions of Windows do not support the property keys of the unified device property model. Instead, these versions of Windows represent these properties by using corresponding system-defined registry entry values under the class registry key. To maintain compatibility with these earlier versions of Windows, Windows Vista and later versions also support these system-defined registry entry values. However, you should use the property keys to access these properties on Windows Vista and later versions.

For a list of the system-defined device setup class properties, see [Device Setup Class Properties That Do Not Have Corresponding SPCRP\_Xxx Identifiers](https://msdn.microsoft.com/library/windows/hardware/ff542250). The device setup class properties are listed by the property key identifiers that you use to access the properties in Windows Vista and later versions. The information that is provided with the property keys also includes the corresponding registry entry values that you can use to access the properties on Windows Server 2003, Windows XP, and Windows 2000.

For information about how to use property keys to access device setup class properties in Windows Vista and later versions, see [Accessing Device Class Properties (Windows Vista and Later)](accessing-device-class-properties--windows-vista-and-later-.md).

To access these properties on Windows Server 2003, Windows XP, and Windows 2000, open the class registry key and use the Windows registry functions to access the registry entry values that correspond to these properties.

To retrieve a handle to the class registry key for a device setup class, call the [**SetupDiOpenClassRegKeyEx**](https://msdn.microsoft.com/library/windows/hardware/ff552067) function and supply the following parameter values:

-   Set *ClassGuid* to a pointer to the GUID that identifies the device setup class of the requested class registry key.

-   Set *samDesired* to a REGSAM-typed value that specifies the required access permission.

-   Set *Flags* to DIOCR\_INSTALLER.

-   Set *MachineName* to a pointer to a NULL-terminated string that contains the name of the computer on which to open the requested class registry key. If the computer is the local computer, set *MachineName* to **NULL**.

-   Set *Reserved* to **NULL**.

If this call to [**SetupDiOpenClassRegKeyEx**](https://msdn.microsoft.com/library/windows/hardware/ff552067) succeeds, **SetupDiOpenClassRegKeyEx** returns the requested handle. If the function call fails, **SetupDiOpenClassRegKeyEx** returns INVALID\_HANDLE\_VALUE and a call to [GetLastError](http://go.microsoft.com/fwlink/p/?linkid=169416) will return the logged error code.

After you retrieve a handle to the class registry key, supply the handle in a call to [RegQueryValueEx](http://go.microsoft.com/fwlink/p/?linkid=95398) and [RegSetValueEx](http://go.microsoft.com/fwlink/p/?linkid=95399) to retrieve or set the registry entry value that corresponds to the device setup class property.

Call the [RegCloseKey](http://go.microsoft.com/fwlink/p/?linkid=194543) function to close the class registry key after access to the key is no longer required.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20Accessing%20Registry%20Entry%20Values%20Under%20the%20Class%20Registry%20Key%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




