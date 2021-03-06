---
title: Obtaining the Original Source Path of an Installed INF File
description: Obtaining the Original Source Path of an Installed INF File
ms.assetid: 7e086248-b11d-43ee-9afa-fad6f2136dc8
keywords: ["SetupAPI functions WDK , INF files", "paths WDK SetupAPI", "INF files WDK SetupAPI", "source paths WDK INF files", "original source paths WDK INF files", "retrieving INF file path information"]
---

# Obtaining the Original Source Path of an Installed INF File


This topic describes how you can retrieve the original source path of an INF file that is installed in the system INF directory. Although there is no [SetupAPI](setupapi.md) function to perform this retrieval directly, you can perform the retrieval indirectly by including entries in an INF file so that the SetupAPI functions that access INF file entries can be used to retrieve the original source path information from an installed INF file.

This method only works for INF files that are installed in the system INF file directory. You cannot use this method for INF files that are present in the [driver store](driver-store.md).

The co-installer that is provided with the toaster sample in the Windows Driver Kit (WDK) uses this method and this topic includes excerpts from the toaster sample that show this method. For more information about the toaster sample, see *toasterpkg.htm*, which is provided in the *src\\general\\toaster* directory of the WDK.

To use this method to retrieve the original source path of an installed INF file, do the following:

1.  Include in the INF file a section that includes an entry whose first field is the %1% string key token. By default, the %1% string key token represents the original source path of the INF file. When Windows installs such an INF file, it saves the original source path string with the installed version of the INF file. Be aware that this method only works if %1% is used as shown in this example. In general, what %1% resolves to is context-dependent. For example, a %1% field in an *add-registry section* entry does not resolve to the original source path; instead %1% in this context resolves to the path of the corresponding INF file in the [driver store](driver-store.md).

2.  Use **SetupOpenInfFile**, **SetupFindFirstLine**, and **SetupGetStringField** to retrieve the original source path from the entry that includes the %1% string key token.

For example, *toasterpkg.inf* includes the following \[ToasterCoInfo\] section with a custom OriginalInfSourcePath entry whose first field is the %1% string key token.

```
[ToastCoInfo]
; Used by the toaster co-installer to figure out where the original media is
; located (so it can start value-added setup programs).
OriginalInfSourcePath = %1%
```

If an INF is configured as illustrated by the toaster sample, you can then retrieve the original source path after installing the INF file in the system INF directory. To retrieve the original source path, first call **SetupOpenInfFile** to open the installed INF file. For example, the following code example from *toastco.c* opens the installed *toasterpkg.inf* file.

```
// Since the INF is already in %SystemRoot%\Inf, we need to find out where it
// originally came from.  There is no direct way to ascertain an INF&#39;s
// path of origin, but we can indirectly determine it by retrieving a field
// from our INF that uses a string substitution of %1% (DIRID_SRCPATH).
//
hInf = SetupOpenInfFile(DriverInfoDetailData->InfFileName,
                        NULL,
                        INF_STYLE_WIN4,
                        NULL
                        );
```

After opening the installed INF file, call **SetupFindFirstLine** to retrieve the first line of the section that contains the entry whose first field is the %1% string key token. Next, call **SetupGetStringField** to retrieve the first field of this entry and retrieve the original source path of the INF file. For example, the following code example from *toastco.c* retrieves the line that contains the custom OriginalInfSourcePath entry and then retrieves the first field of this entry. Because the first field in the original INF is the %1% string key token, **SetupGetStringField** returns the original source path of the INF file.

```
// Contained within our INF should be a [ToastCoInfo] section with the
// following entry:
//
//     OriginalInfSourcePath = %1%
//
// If we retrieve the value (i.e., field 1) of this line, we&#39;ll get the
// full path where the INF originally came from.
//
if(!SetupFindFirstLine(hInf, L"ToastCoInfo", L"OriginalInfSourcePath", &amp;InfContext)) {
   goto clean0;
}
if(!SetupGetStringField(&amp;InfContext, 1, *MediaRootDirectory, MAX_PATH, &amp;PathLength) ||
  (PathLength <= 1)) {
  goto clean0;
```

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20Obtaining%20the%20Original%20Source%20Path%20of%20an%20Installed%20INF%20File%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




