---
title: Identifiers for PCMCIA Devices
description: Identifiers for PCMCIA Devices
ms.assetid: 7eaf6372-a9cc-4714-8955-52653ec57141
keywords: ["device identification strings WDK , PCMCIA devices", "identification strings WDK device , PCMCIA devices", "identifiers WDK device , PCMCIA devices", "PCMCIA device identifiers WDK device installations", "device IDs WDK device installations", "hardware IDs WDK device installations", "compatible IDs WDK device installations"]
---

# Identifiers for PCMCIA Devices


## <a href="" id="ddk-identifiers-for-pcmcia-devices-dg"></a>


For Personal Computer Memory Card International Association (PCMCIA) devices, the device ID can take several different forms. For devices that are not multifunctional, the device identifier is formatted as follows:

PCMCIA\\Manufacturer-Product-Crc(4)

Where:

-   *Manufacturer* is the name of the manufacturer.

-   *Product* is the name of the product.

The PCMCIA enumerator retrieves these strings directly from tuples on the card. Both *Manufacturer* and *Product* are variable-length strings that do not exceed 64 characters. *Crc(4)* is the 4-digit hexadecimal CRC (cyclic redundancy check) checksum for the card. Numbers less than four digits long have a leading zero fill. For example, the device ID for a network adapter might be this:

PCMCIA\\MEGAHERTZ-CC10BT/2-BF05

For a multifunction card, every function has an identifier of the form:

PCMCIA\\Manufacturer-Product-DEVd(4)-Crc(4)

The child function number (*d(4)* in this example) is a decimal number without leading zeros.

If the card does not have a name of the manufacturer, the identifier has one of these three forms:

PCMCIA\\UNKNOWN\_MANUFACTURER-Crc(4)

PCMCIA\\UNKNOWN\_MANUFACTURER-DEVd(4)-Crc(4)

PCMCIA\\MTD-MemoryType(4)

The last of these three alternatives is for a flash memory card without a manufacturer identifier on the card. *MemoryType(4)* is one of two 4-digit hexadecimal numbers: 0000 for SRAM cards and 0002 for ROM cards.

In addition to the various forms of device ID just described, an INF file's [**Models section**](inf-models-section.md) can also contain a hardware ID composed by replacing the 4-digit hexadecimal cyclic redundancy check (CRC) with a string that contains the 4-digit hexadecimal manufacturer code, a hyphen, and the 4-digit hexadecimal manufacturer information code (both from on-board tuples). For example:

PCMCIA\\MEGAHERTZ-CC10BT/2-0128-0103

PCMCIA-compatible IDs correspond to the generic device IDs mentioned in the [Generic Identifiers](generic-identifiers.md) section. Currently, PCMCIA-compatible IDs are generated for only three device types as described in the following table.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">PCMCIA-compatible ID</th>
<th align="left">Device type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>*PNP0600</p></td>
<td align="left"><p>An AT Attachment (ATA) disk driver</p></td>
</tr>
<tr class="even">
<td align="left"><p>*PNP0D00</p></td>
<td align="left"><p>A multifunction 3.0 PC Card</p></td>
</tr>
<tr class="odd">
<td align="left"><p>*PNPC200</p></td>
<td align="left"><p>A modem card</p></td>
</tr>
</tbody>
</table>

 

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20Identifiers%20for%20PCMCIA%20Devices%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




