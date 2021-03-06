---
title: Guidelines for Using SetupAPI
description: Guidelines for Using SetupAPI
ms.assetid: a5005a4e-206a-4971-b89d-0d8f833d38c8
keywords: ["SetupAPI functions WDK , guidelines", "device installation functions WDK SetupAPI", "general Setup functions WDK SetupAPI"]
---

# Guidelines for Using SetupAPI


## <a href="" id="ddk-guidelines-for-using-setupapi-dg"></a>


The following are guidelines for using the [general Setup functions](https://msdn.microsoft.com/library/windows/hardware/ff544985) (**Setup***Xxx*) and [device installation functions](https://msdn.microsoft.com/library/windows/hardware/ff541299) (**SetupDi***Xxx*) that are provided by SetupAPI:

-   Never assume that installation file contents are error-free, or that an installation file that you provided hasn't been maliciously modified. Therefore, always validate all information received from SetupAPI functions. Verify that strings are of valid length, that buffers are of valid size, and that index values are within a valid range.

-   When writing installation applications for installations on Microsoft Windows XP and later systems, you can call **SetupVerifyInfFile** (described in the Windows SDK documentation), which verifies that a digitally signed INF file has not been modified.

-   Always test the return value of each SetupAPI function. If the function fails, your code should call [GetLastError](http://go.microsoft.com/fwlink/p/?linkid=169416) to obtain an error code that identifies the failure. Returned error codes can be defined in *Winerror.h* or *Setupapi.h*. Before calling **FormatMessage** with FORMAT\_MESSAGE\_FROM\_SYSTEM to create a text display, always use the HRESULT\_FROM\_SETUPAPI macro (defined in *Winerror.h*) to convert the return value to an HRESULT value. If a SetupAPI function returns successfully, your code must not call [GetLastError](http://go.microsoft.com/fwlink/p/?linkid=169416). (The [GetLastError](http://go.microsoft.com/fwlink/p/?linkid=169416) and **FormatMessage** functions, together with system error codes, are described in the Windows SDK documentation.)

-   If a SetupAPI function returns a handle, your code must check for a return value of INVALID\_HANDLE\_VALUE. Such functions do not return **NULL**.

-   Be aware of the following difference between the **SetupDi***Xxx* and **Setup***Xxx* functions that allow a caller to query for the required size of a buffer:

    -   If the caller of a **SetupDi***Xxx* function makes such a query, [GetLastError](http://go.microsoft.com/fwlink/p/?linkid=169416) always returns ERROR\_INSUFFICIENT\_BUFFER.

    -   If the caller of a **Setup***Xxx* function makes such a query, [GetLastError](http://go.microsoft.com/fwlink/p/?linkid=169416) returns NO\_ERROR if no buffer length was specified or ERROR\_INSUFFICIENT\_BUFFER if a buffer was specified that was too small.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20Guidelines%20for%20Using%20SetupAPI%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




