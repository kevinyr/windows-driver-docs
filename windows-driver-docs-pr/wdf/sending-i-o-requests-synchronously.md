---
title: Sending I/O Requests Synchronously
author: windows-driver-content
description: Sending I/O Requests Synchronously
ms.assetid: e7e9f2d2-afc5-439b-8a04-72d117114fae
keywords: ["general I/O targets WDK KMDF , sending I/O requests to", "sending I/O requests WDK KMDF", "sending I/O requests WDK KMDF , synchronous", "synchronously sending I/O requests WDK KMDF"]
---

# Sending I/O Requests Synchronously


## <a href="" id="ddk-sending-i-o-requests-synchronously-df"></a>


The following table lists the I/O target object methods that your driver can call to send I/O requests synchronously to an I/O target. For detailed information about how to use these methods, see the methods' reference pages.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Method</th>
<th align="left">Purpose</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[<strong>WdfIoTargetSendReadSynchronously</strong>](https://msdn.microsoft.com/library/windows/hardware/ff548669)</p></td>
<td align="left"><p>Sends a read request</p></td>
</tr>
<tr class="even">
<td align="left"><p>[<strong>WdfIoTargetSendWriteSynchronously</strong>](https://msdn.microsoft.com/library/windows/hardware/ff548672)</p></td>
<td align="left"><p>Sends a write request</p></td>
</tr>
<tr class="odd">
<td align="left"><p>[<strong>WdfIoTargetSendIoctlSynchronously</strong>](https://msdn.microsoft.com/library/windows/hardware/ff548660)</p></td>
<td align="left"><p>Sends a device control request</p></td>
</tr>
<tr class="even">
<td align="left"><p>[<strong>WdfIoTargetSendInternalIoctlSynchronously</strong>](https://msdn.microsoft.com/library/windows/hardware/ff548656)</p></td>
<td align="left"><p>Sends an internal device control request</p></td>
</tr>
<tr class="odd">
<td align="left"><p>[<strong>WdfIoTargetSendInternalIoctlOthersSynchronously</strong>](https://msdn.microsoft.com/library/windows/hardware/ff548651)</p></td>
<td align="left"><p>Sends a non-standard internal device control request</p></td>
</tr>
</tbody>
</table>

 

You can also send requests synchronously by calling [**WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027), but you have to format the request first by following the rules that are described in [Sending I/O Requests Asynchronously](sending-i-o-requests-asynchronously.md).

Sending I/O requests to an I/O target synchronously is simpler to program than sending I/O requests [asynchronously](sending-i-o-requests-asynchronously.md). However, you should use the following guidelines to help you decide if synchronous I/O is appropriate for your driver:

-   You can use synchronous I/O if your driver does not send many I/O requests and if system or device performance is not reduced because your driver waits for each I/O request to complete.

-   If your driver must handle many I/O requests in short periods of time, you probably cannot allow your driver to wait for each request to complete before sending the next request. Otherwise, your driver might lose data or reduce the performance of its device (and, possibly, the entire system). In such cases, asynchronous I/O might be the better choice.

-   Synchronous I/O is useful for handling operations that must start and finish without additional concurrent activity. Such operations might include resetting a USB pipe or reading device registers.

-   Most times, your driver should specify a time-out value when it calls an object method that sends an I/O request synchronously. If your driver does not specify a time-out value, and if a device or a lower-level driver fails to respond, your driver can stall. As a result, the user can experience an unresponsive application. In addition, other drivers might not be able to obtain system resources, such as [work items](using-framework-work-items.md), if your driver is not releasing them.

-   If drivers above and below yours in the stack require operations to proceed synchronously, your driver should use synchronous I/O. Therefore, you should learn about the requirements of other drivers that might exist in the driver stack.

The following example shows how to send a synchronous I/O control (IOCTL) request:

```
NTSTATUS                status;
    WDF_MEMORY_DESCRIPTOR   inputDesc, outputDesc;
    PWDF_MEMORY_DESCRIPTOR  pInputDesc = NULL, pOutputDesc = NULL;
    ULONG_PTR               bytesReturned;

    UNREFERENCED_PARAMETER(FileObject);

    if (InputBuffer) {
        WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(&amp;inputDesc,
                                    InputBuffer,
                                    InputBufferLength);
        pInputDesc = &amp;inputDesc;
    }

    if (OutputBuffer) {
        WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(&amp;outputDesc,
                                    OutputBuffer,
                                    OutputBufferLength);
        pOutputDesc = &amp;outputDesc;
    }

    status = WdfIoTargetSendIoctlSynchronously(
                        IoTarget,
                        WDF_NO_HANDLE, // Request
                        IoctlControlCode,
                        pInputDesc,
                        pOutputDesc,
                        NULL, // PWDF_REQUEST_SEND_OPTIONS
                        &amp;bytesReturned);
    if (!NT_SUCCESS(status)) {
         DEBUGP(MP_ERROR,
        ("WdfIoTargetSendIoctlSynchronously failed 0x%x\n",
          status));
    }

    *BytesReadOrWritten = (ULONG)bytesReturned;
```

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bwdf\wdf%5D:%20Sending%20I/O%20Requests%20Synchronously%20%20RELEASE:%20%284/5/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




