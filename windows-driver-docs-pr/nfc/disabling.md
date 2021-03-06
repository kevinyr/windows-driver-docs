---
title: Disabling NFP
author: windows-driver-content
description: A client can temporarily disable subscriptions, publications, and presence.
ms.assetid: 94BE6D24-60AD-45BD-AF2D-388022114975
keywords: ["NFC", "near field communications", "proximity", "near field proximity", "NFP"]
---

# Disabling NFP


A client can temporarily disable subscriptions, publications, and presence.

Temporarily disabling subscriptions, publications, and presence is done by sending [**IOCTL\_NFP\_DISABLE**](https://msdn.microsoft.com/library/windows/hardware/jj853315) to the handle. This is useful when a client wants to disable the proximity functionality but keep the resources allocated to quickly re-enable them when needed.

 

 
## Related topics
[NFC device driver interface (DDI) overview](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[Near field proximity DDI reference](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnfpdrivers\nfpdrivers%5D:%20Disabling%20NFP%20%20RELEASE:%20%284/5/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")
