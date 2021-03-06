---
title: File Streams, Stream Contexts, and Per-Stream Contexts
author: windows-driver-content
description: File Streams, Stream Contexts, and Per-Stream Contexts
ms.assetid: baea4967-f0d6-4096-aac4-fd38c117b4c6
keywords: ["filter drivers WDK file system , per-stream context tracking", "file system filter drivers WDK , per-stream context tracking", "per-stream context tracking WDK file system", "tracking per-stream context WDK file system", "file streams WDK", "stream control blocks WDK file system", "SCB WDK file system", "stream context WDK file system"]
---

# File Streams, Stream Contexts, and Per-Stream Contexts


## <span id="ddk_file_streams_stream_contexts_and_per_stream_contexts_if"></span><span id="DDK_FILE_STREAMS_STREAM_CONTEXTS_AND_PER_STREAM_CONTEXTS_IF"></span>


A *file stream* is a sequence of bytes used to hold file data. Usually a file has only one file stream, namely the file's default data stream. However, on file systems that support multiple data streams, each file can have multiple file streams. One of these is the default data stream, which is unnamed. The others are named alternate data streams. When you open a file, you are actually opening a stream of the given file.

When a file system opens a file stream for the first time, it creates a file-system-specific *stream context* structure, such as a file control block (FCB) or stream control block (SCB), and stores the address of this structure in the **FsContext** member of the resulting file object.

For local file systems, if the already opened file stream is opened again (for shared read access, for example), the I/O subsystem creates another file object, but the file system does not create a new stream context. Both file objects receive the address of the same stream context structure. Thus, for local file systems, the stream context pointer uniquely identifies a file stream.

For network file systems that support per-stream contexts, if the already opened file stream is opened again using the same network share name or IP address, the behavior is the same as for local file systems. The I/O subsystem creates a new file object, but the file system does not create a new stream context. Instead, it assigns the same **FsContext** pointer value to both file objects. However, if the file stream is opened using a different path (for example, a different share name, or an IP address for a file previously opened using a share name), the file system does create a new stream context. Thus, for network file systems that support per-stream contexts, the **FsContext** pointer does not uniquely identify a file stream.

A *per-stream context* is a filter-defined structure that contains a [**FSRTL\_PER\_STREAM\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547357) structure as one of its members. Filter drivers use this structure to track information about each file stream that is opened by the file system.

### <span id="File_System_Support_for_Per-Stream_Contexts"></span><span id="file_system_support_for_per-stream_contexts"></span><span id="FILE_SYSTEM_SUPPORT_FOR_PER-STREAM_CONTEXTS"></span>File System Support for Per-Stream Contexts

On Microsoft Windows XP and later, file systems that support per-stream contexts must use stream context structures that contain a [**FSRTL\_ADVANCED\_FCB\_HEADER**](https://msdn.microsoft.com/library/windows/hardware/ff547334) structure.

The global list of per-stream contexts associated with a particular file stream is owned by the file system. When the file system creates a new stream context (FSRTL\_ADVANCED\_FCB\_HEADER object) for a file stream, it calls [**FsRtlSetupAdvancedHeader**](https://msdn.microsoft.com/library/windows/hardware/ff547257) to initialize this list. When a file system filter driver calls [**FsRtlInsertPerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff546194), the per-stream context created by the filter is added to the global list.

When the file system deletes its stream context for a file stream, it calls [**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295) to free all per-stream contexts that filters have associated with the file stream. This routine calls the [**FreeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff547357) routine for each per-stream context in the global list. Note that the **FreeCallback** routine must assume that the file object for the file stream has already been freed.

To query whether the file system supports per-stream contexts for the file stream represented by a given file object, call [**FsRtlSupportsPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547285) on the file object. Note that a file system might support per-stream contexts for some types of files but not for others. For example, NTFS and FAT do not currently support per-stream contexts for paging files. Thus if **FsRtlSupportsPerStreamContexts** returns **TRUE** for one file stream, this does not imply that it returns **TRUE** for all file streams.

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[ifsk\ifsk]:%20File%20Streams,%20Stream%20Contexts,%20and%20Per-Stream%20Contexts%20%20RELEASE:%20%285/9/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


