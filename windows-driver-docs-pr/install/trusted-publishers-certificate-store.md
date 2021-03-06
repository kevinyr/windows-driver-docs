---
title: Trusted Publishers Certificate Store
description: Trusted Publishers Certificate Store
ms.assetid: e2fcb0ce-82e3-499a-85b9-76e4e742190e
keywords: ["driver signing WDK , Trusted Publishers certificate store", "Trusted Publishers certificate store WDK", "certificate stores WDK"]
---

# Trusted Publishers Certificate Store


The *Trusted Publishers certificate store* contains information about the Authenticode (signing) certificates of trusted publishers that are installed on a computer. In order to test and debug your [driver packages](driver-packages.md) within your organization, your company should install the Authenticode certificates that are used to sign driver packages in the Trusted Publishers certificate store. Install the Authenticode certificates on each computer in the workgroup or organizational unit that runs signed code. The name of the Trusted Publishers certificate store is *trustedpublisher.*

If a publisher's Authenticode certificate is in the Trusted Publishers certificate store, Windows installs a [driver package](driver-packages.md) that was digitally signed by the certificate without prompting the user (*silent install*). By installing the Authenticode certificates in the Trusted Publishers certificate store, you can automate the installation of your driver package on various systems that are used for internal testing and debugging.

**Important**  This practice of automating the installation of driver packages is only suggested for your internal systems. This practice should never be followed for any driver package that is distributed outside your organization.

 

The Trusted Publishers certificate store differs from the [Trusted Root Certification Authorities certificate store](trusted-root-certification-authorities-certificate-store.md) in that only *end-entity* certificates can be trusted. For example, if an Authenticode certificate from a CA was used to [test-sign](introduction-to-test-signing.md) a driver package, adding that certificate to the Trusted Publishers certificate store does not configure all certificates that this CA issued as trusted. Each certificate must be added separately to the Trusted Publishers certificate store.

Use a Group Policy to distribute certificates to an organizational unit on a network. In this situation, the administrator adds a Certificate Rule to a Group Policy to establish trust in a publisher. Certificate Rules are part of the software restriction policies that are supported on the following Windows versions:

-   Windows Vista and later versions of Windows.

-   Windows Server 2003.

You can manually install the Authenticode certificates into the Trusted Publishers certificate store on a computer by using the [**CertMgr**](https://msdn.microsoft.com/library/windows/hardware/ff543411) tool.

**Note**  The driver signing verification policy used by Plug and Play requires that the Authenticode certificate of a CA has been previously installed in the local machine version of the Trusted Publishers certificate store. For more information, see [Local Machine and Current User Certificate Stores](local-machine-and-current-user-certificate-stores.md).

 

For more information about software restriction policies and using Certificate Rules, see the information in the Windows Help and Support Center. In addition, you find more information about these topics on the [Microsoft TechNet](http://go.microsoft.com/fwlink/p/?linkid=10111) website.

For more information about how to deploy Authenticode certificates in an enterprise by using Group Policy, see the readme file *Selfsign\_readme.htm*, which is located in the *src\\general\\build\\driversigning* directory of the WDK.

For more information about certificate stores, see the [Code Signing Best Practices](http://go.microsoft.com/fwlink/p/?linkid=68250) website.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20Trusted%20Publishers%20Certificate%20Store%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




