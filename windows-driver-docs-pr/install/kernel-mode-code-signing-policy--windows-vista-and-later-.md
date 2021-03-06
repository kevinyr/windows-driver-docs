---
title: Driver Signing Policy
description: Driver Signing Policy
ms.assetid: c3ba672c-5bf2-4885-a85e-fa6d8a47ca54
keywords: ["driver signing WDK , kernel-mode code signing policy", "signing drivers WDK , kernel-mode code signing policy", "digital signatures WDK , kernel-mode code signing policy", "signatures WDK , kernel-mode code signing policy", "kernel-mode code signing policy WDK", "kernel-mode driver signing WDK", "driver package digital signatures WDK", "package digital signatures WDK"]
---

# Driver Signing Policy


Starting with 64-bit versions of Windows Vista and later versions of Windows, driver code signing policy requires that all driver code have a digital signature. In addition, certain configurations of 32-bit versions of Windows Vista and later versions of Windows also require driver code to be digitally-signed in order to access next generation premium content that is controlled by the content protection policy. Windows Vista and later versions of Windows rely on digital signatures of these components to increase the safety and stability of the Microsoft Windows platform and enable new customer experiences with next generation premium content.

**Note**  Windows 10 for desktop editions (Home, Pro, Enterprise, and Education) and Windows Server 2016 kernel-mode drivers must be signed by the Windows Hardware Dev Center Dashboard and the Windows Hardware Dev Center Dashboard requires an EV certificate. For more info about these changes, see [Driver Signing Changes in Windows 10](http://blogs.msdn.com/b/windows_hardware_certification/archive/2015/04/01/driver-signing-changes-in-windows-10.aspx).

 

Digital signatures allow the administrator or end-user who is installing Windows-based software to know whether a legitimate publisher has provided the software package. When users choose to send Windows Error Reporting data to Microsoft after a fault or other error occurs, Microsoft can analyze the data to know which publishers' software was running on the system at the time of the error. Software publishers can then use the information that is provided by Microsoft to find and fix problems in their software.

The driver code signing policy starting with Windows Vista and later versions of Windows requires that the following types of drivers have digital signatures:

-   For 64-bit versions of Windows, all kernel mode software, including, but not limited to, kernel-mode device drivers.

    **Note**  Windows 10 for desktop editions and Windows Server 2016 kernel-mode drivers must be signed by the Windows Hardware Dev Center Dashboard and the Windows Hardware Dev Center Dashboard requires an EV certificate.

     

-   For 64-bit versions of Windows, user mode drivers, such as printer drivers.

-   Drivers that stream protected content. This includes audio drivers that use Protected User Mode Audio (PUMA) and Protected Audio Path (PAP), and video device drivers that handle protected video path-output protection management (PVP-OPM) commands. Information about these requirements is outside the scope of this documentation. For more information about these requirements, see [Code-signing for Protected Media Components (Windows Vista and Later)](http://go.microsoft.com/fwlink/p/?linkid=74262).

Starting with Windows 8 UEFI Secure Boot-enabled platforms have additional signing requirements, including requirements for ARM platforms. The driver code signing policy for 32-bit versions of Windows 8 UEFI Secure Boot-enabled platforms also requires drivers have a digital signature.

The following table lists the signature requirements for different types of drivers based on processor architecture and Secure Boot state.

Secure Boot Enabled
Secure Boot Disabled
x86
x64
ARM
x86
x64
ARM
Kernel Mode Drivers

3rd party boot drivers

**Signature Algo**

SHA1 or above

**Signature type**

Embedded

**Signature requirement**

Microsoft Root Authority 2010

WHQL signature required

**Signature Algo**

SHA256

**Signature type**

Embedded

**Signature requirement**

Microsoft Root Authority 2010

WHQL Signature Required

Unsigned drivers allowed

**Signature Algo**

SHA1 or above

**Signature type**

Embedded or catalog signed

**Signature requirement**

Standard roots trusted by CI

N/A (Secure Boot cannot be disabled)

ELAM

ELAM drivers must be signed by the process described [here](http://msdn.microsoft.com/library/windows/desktop/hh848061.aspx).

Drivers

**Signature Algo**

SHA1 or above

**Signature type**

Embedded

**Signature requirement**

Microsoft Root Authority 2010

WHQL signature required

**Signature Algo**

SHA256

**Signature type**

Embedded

**Signature requirement**

Microsoft Root Authority 2010

WHQL Signature Required

Unsigned drivers allowed

**Signature Algo**

SHA1 or above

**Signature type**

Embedded or catalog signed

**Signature requirement**

Standard roots trusted by CI

N/A (Secure Boot cannot be disabled)

 

Be aware that this code signing policy is in addition to the [Plug and Play (PnP) device installation signing requirements](pnp-device-installation-signing-requirements--windows-vista-and-later-.md) that affect the installation of a device driver. A developer and publisher of a driver must comply with both the driver code signing requirement for loading a kernel-mode driver and the PnP device installation signing requirements for installing a driver. Also be aware that, although an administrator can authorize the preinstallation of an unsigned kernel-mode driver on a 64-bit system, the administrator cannot subsequently load the unsigned driver during the installation of the driver for a device.

Starting with Windows Vista, driver code signing enforcement is implemented by a component known as Code Integrity. Code Integrity is a feature that improves the security of the operating system by verifying the integrity of a file every time that the image of the file is loaded into memory. The function of Code Integrity is to detect if an unsigned driver is being loaded into kernel-mode, or if a system binary file has been modified by malicious code that may have been run by an administrator.

Starting with Windows Vista, Code Integrity helps ensure that the operating system is running known, identifiable code. Code Integrity generates diagnostic events and a system audit log event when the signature of a kernel module fails to verify correctly. You can use the information logged by Code Integrity to [troubleshoot driver load problems](troubleshooting-install-and-load-problems-with-signed-driver-packages.md).

For development and testing purposes only, enforcement of the driver code signing policy can be temporarily disabled. For more information, see [Installing an Unsigned Driver Package during Development and Test](installing-an-unsigned-driver-during-development-and-test.md).

For general information about how to sign a driver for public release on Windows Vista and later versions of Windows, see [Signing Drivers for Public Release (Windows Vista and Later)](signing-drivers-for-public-release--windows-vista-and-later-.md).

For general information about how to test-sign a driver during development and test on Windows Vista and later versions of Windows, see [Signing Drivers during Development and Test (Windows Vista and Later)](signing-drivers-during-development-and-test--windows-vista-and-later-.md).

For more information about driver code signing requirements, see the [Digital Signatures for Kernel Modules on Systems Running Windows Vista](http://go.microsoft.com/fwlink/p/?linkid=184997) website.

**Note**  The information that is provided at that website is also applicable to Windows Server 2008and later versions of Windows.

 

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20Driver%20Signing%20Policy%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




