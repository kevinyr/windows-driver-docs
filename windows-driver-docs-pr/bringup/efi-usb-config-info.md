---
title: EFI\_USB\_CONFIG\_INFO
author: windows-driver-content
description: EFI\_USB\_CONFIG\_INFO
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 74d5cb02-2648-4bd1-990e-61156b5dc8cd
---

# EFI\_USB\_CONFIG\_INFO


The **EFI\_USB\_CONFIG\_INFO** structure is used to define the supported USB port configuration.

## Syntax


``` syntax
typedef struct 
{
    EFI_USB_CONFIG_DESCRIPTOR           *ConfigDescriptor;
    EFI_USB_INTERFACE_INFO              **InterfaceInfoTable;
} EFI_USB_CONFIG_INFO;
```

## Members


<a href="" id="configdescriptor"></a>**ConfigDescriptor**  
An EFI\_USB\_CONFIG\_DESCRIPTOR structure that contains configuration information for the USB function device.

<a href="" id="interfaceinfotable"></a>**InterfaceInfoTable**  
An [EFI\_USB\_INTERFACE\_INFO](efi-usb-interface-info.md) structure that contains information about the supported interfaces.

## Remarks


The structure **USB\_CONFIG\_DESCRIPTOR** is defined in UEFI specification 2.3. For more information, visit the [UEFI.org](http://go.microsoft.com/fwlink/p/?linkid=109526) website.

## Requirements


**Header:** User generated

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_OEMBringUp\p_oembringup%5D:%20EFI_USB_CONFIG_INFO%20%20RELEASE:%20%284/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


