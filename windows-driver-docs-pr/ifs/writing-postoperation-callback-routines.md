---
title: Writing Postoperation Callback Routines
author: windows-driver-content
description: Writing Postoperation Callback Routines
ms.assetid: 4940e38d-107b-45c4-aa71-6e8543330f39
keywords: ["postoperation callback routines WDK file system minifilter , writing", "writing callback routines"]
---

# Writing Postoperation Callback Routines


## <span id="ddk_writing_postoperation_callback_routines_if"></span><span id="DDK_WRITING_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


A file system minifilter driver uses one or more *postoperation callback routines* to filter I/O operations.

A postoperation callback routine can take one of the following actions:

-   Accomplish completion work directly in postoperation routine. All the completion work can be accomplished at IRQL &lt;= DISPATCH\_LEVEL.
-   Accomplish completion work at a safe IRQL. Return FLT\_STATUS\_MORE\_PROCESSING\_REQUIRED and queue a worker thread to allow processing at safe IRQL. When processing is complete, the worker thread calls [**FltCompletePendedPostOperation**](https://msdn.microsoft.com/library/windows/hardware/ff541897) to continue postoperation processing.
-   Cancel a successful CREATE operation.

[**Postoperation callback routines**](https://msdn.microsoft.com/library/windows/hardware/ff551107) are similar to the *completion routines* that are used in legacy file system filter drivers.

A minifilter driver registers a postoperation callback routine for a particular type of I/O operation in the same way it registers a [**preoperation callback routine**](https://msdn.microsoft.com/library/windows/hardware/ff551109)—that is, by storing the callback routine's entry point in the **OperationRegistration** member of the [**FLT\_REGISTRATION**](https://msdn.microsoft.com/library/windows/hardware/ff544811) structure that the minifilter driver passes as a parameter to [**FltRegisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544305) in its **DriverEntry** routine.

Minifilter drivers receive only those types of I/O operations for which they have registered a preoperation or postoperation callback routine. A minifilter driver can register a preoperation callback routine for a given type of I/O operation without registering a postoperation callback, and vice versa.

Every postoperation callback routine is defined as follows:

```
typedef FLT_POSTOP_CALLBACK_STATUS 
(*PFLT_POST_OPERATION_CALLBACK) ( 
    IN OUT PFLT_CALLBACK_DATA Data, 
    IN PCFLT_RELATED_OBJECTS FltObjects, 
    IN PVOID CompletionContext, 
    IN FLT_POST_OPERATION_FLAGS Flags 
    ); 
```

Like a completion routine, a postoperation callback routine is called at IRQL &lt;= DISPATCH\_LEVEL, in an arbitrary thread context.

Because it can be called at IRQL = DISPATCH\_LEVEL, a postoperation callback routine cannot call kernel-mode routines that must be called at a lower IRQL, such as [**FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371) or [**RtlCompareUnicodeString**](https://msdn.microsoft.com/library/windows/hardware/ff561782). For the same reason, any data structures that are used in a postoperation callback routine must be allocated from nonpaged pool.

The following situations are several exceptions to the preceding rule:

-   If a minifilter driver's preoperation callback routine returns FLT\_PREOP\_SYNCHRONIZE for an IRP-based I/O operation, the corresponding postoperation callback routine is called at IRQL &lt;= APC\_LEVEL, in the same thread context as the preoperation callback routine.

-   The postoperation callback routine for a fast I/O operation is called at IRQL = PASSIVE\_LEVEL, in the same thread context as the preoperation callback routine.

-   Post-create callback routines are called at IRQL = PASSIVE\_LEVEL, in the context of the thread that originated the IRP\_MJ\_CREATE operation.

When the filter manager calls a minifilter driver's postoperation callback routine for a given I/O operation, the minifilter driver temporarily controls the I/O operation. The minifilter driver retains this control until it does one of the following:

-   Returns FLT\_POSTOP\_FINISHED\_PROCESSING from the postoperation callback routine.

-   Calls [**FltCompletePendedPostOperation**](https://msdn.microsoft.com/library/windows/hardware/ff541897) from a work routine that has processed an IRP-based I/O operation that was pended in the postoperation callback routine.

This section includes:

[Performing Completion Processing for an I/O Operation](performing-completion-processing-for-an-i-o-operation.md)

[Pending an I/O Operation in a Postoperation Callback Routine](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)

[Failing an I/O Operation in a Postoperation Callback Routine](failing-an-i-o-operation-in-a-postoperation-callback-routine.md)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[ifsk\ifsk]:%20Writing%20Postoperation%20Callback%20Routines%20%20RELEASE:%20%285/9/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


