# CPC464 iRAM/1024

> [!IMPORTANT]
>**An incompatibility with the M4 board of the initital release of the iRAM/1024 has been reported. This has been fixed with this new revision. If you built the initital version it's possible to apply some small modifications to make it compatible with the M4.**
> See  [the README of rev1](README_rev1.md) for more details. 



<!--
> [!TIP]
> PCBs can be ordered at [PCBWay](https://www.pcbway.com/project/shareproject/CPC_iRAM_1024_1MB_internal_RAM_expansion_for_the_Amstrad_CPC_464_and_664_9310ac8d.html) with a few clicks. Recommended PCB thickness is 1.2mm.
-->

The iRAM/1024 is an internal RAM expansion for the Amstrad CPC 464 and CPC 664 which upgrades the computer to a total of 1024KB - sixteen times the amount of the original 64KB. 

It even supports [C3 paging mode](http://norecess.cpcscene.net/advancedmemoryusage.html) which allows you to run CP/M plus, FutureOS or some games and demos with C3 requirement (e.g Pac-Man emulator or the demos PHX and Phortem).

<img src="/pictures/installed464board1.jpg" width="640"/>

Legacy software that supports the DK'Tronics memory standard will be able to access up to 576K of RAM ([the maximum suppored by DK'Tronics](https://www.cpcwiki.eu/index.php/Standard_Memory_Expansions#Standard_128K-512K_Expansions_.28dk.27tronics.2Fdobbertin-style.29)). More recent software, like e.g. SymbOS, with support for the [enhanced Yarek/RAM7 standard](https://www.cpcwiki.eu/index.php/Standard_Memory_Expansions#Extended_1M-4M_Expansions_.28RAM7.2FYarek-style.29) will see the full 1024K. 

> [!IMPORTANT]
> 
> This version will properly work only in the Amstrad CPC 464 and 664. It will not work in the Amstrad Plus and GX4000 models and can potentially cause harm to them.
> 
> The PCB was designed so it fits into all known variations of the 464 and 664. It has been confirmed to fit into the 664, 464 motherboard version 1,2 and 3. On board revision 3 it can be necessary to bend the Gate Array cooling plate slightly (see below). 
> A final confirmation that it also fits 464 version 4 (cost reduced with ASIC) is still pending as I don't own that one and couldn't source it yet. Please let me know if you can confirm that it fits/doesn't fit this version.
> 
> It won't fit into the CPC 6128 due to space constraints in the 6128. There are two specific CPC6128 versions, iRAM/640 and iRAM/1088. See other projects on this Github profile. 

## Variations

The same PCB supports 3 RAM configurations: 

- total of 1024K RAM (64K base + 960K extended memory): 2x 512K SRAM, C3 support <b>recommended config<sup>*</sup></b>
- total of 1088K RAM (64K base + 1024K extended memory): 2x 512K SRAM, <b>no C3</b>
- total of 576K RAM (64K base + 512K extended memory), 1x 512K SRAM, <b>no C3</b>

Due to a lack of pins of the CPLDs this cannot be selected and the CPLDs need to be programmed for either C3 or non-C3 support. 
 
<sup>*: If there is no specific need to avoid C3 or to have the full 1024 of expanded RAM this is probably the best config as it enables optimal 6128 compatibility. Some tech demos might that do not test for available RAM blocks and simply expect the full SRAM to be available might have issues though.</sup>

## Goals

Main goals of this expansions were:
- fits into a standard CPC 464 and 664
- full CPC 6128 compatibility ([C3 paging mode](http://norecess.cpcscene.net/advancedmemoryusage.html)) to support CP/M plus, Future-OS and games/demos with C3 requirement.  
- requires no internal modifications, especially no additional internal soldering
- DIY friendly
	- all easy-to solder through-hole components
	- no FPGA, CPLDs can be programmed with many cheap EPROM programmers
- cheap - all components should be available for €20 or less in total
- long-term availability - all components are still manufactured and will probably be available for decades (at least as NOS)

## License

The expansion and all resources are free to use for personal use.

It is released under the CC BY-NC-ND 4.0 license with the following exception: Commercial production and selling is permitted (and encouraged) as long as the final product will be sold for a maximum of USD 40 / €40 / £38 or the equivalent in other currencies (excl. shipping and platform fees like e.g. for Ebay or SellMyRetro). 
<sub>Considering the cost of the components (especially when bought in quantities) and the time required for the assembly, this should be sufficient for an interesting profit margin while keeping the expansion affordable for the community.</sub> 

## Support

There is no official support. If you have any questions feel free to join the "Technical support - Hardware related" board on the cpcwiki.eu forum.

### Known issues

- In some CPC 464 (motherboard rev. 3 with GateArray 40007 fitted) the heat sink of the Gate Array might block the installation. The heat sink needs to be bent or replaced. See below for details.
- On beta tester reported crashes in BATMAN demo. These could be resolved with a different CPU. It has not been clear what has caused the issue. It might be due to lack of power through the CPU socket. If you experience the issue try cleaning the CPU socket and properly placing the iRAM into the socket to limit resistance. If this won't help replace the 22uF cap with a 47uF cap and/or connect the spare 5V/GND pins (bottom left side of the PCB) to a 5V and GND pin on the motherboard. Please reach out via "Issues" or the CPC Wiki if you experience the issue and share if/how you could solve it.
- Not really an issue but working as designed: With C3 emulation active the upper most 64K of the secondary SRAM are used for said C3 emulation and are not available for applications or programs. Software therefore can access 64K base RAM + 960K expanded RAM (not 1024K). Properly designed software like SymbOS that tests the availability of RAM banks before using them will not be impacted but if software just assumes that a full 1024K of expansion RAM are present they might experience crashes once software accesses this RAM area. As that much RAM is only used by a few tech demos, FutureOS and SymbOS, the real world relevance is negligible, especially since SymbOS is limited to a total memory size of 1MB and won't be able to use the upper most 64K anyway. If it's relevant to have the full 1024K just use the alternative JED file for PAL3 which removes C3 emulation but gives access to the full 1024K.
  
## Building the expansion

For a full assembly you need 
- basic soldering skills - as long as you can solder normal through hole components reliably, you will be fine.
- an option to program ATF16V8 CPLDs. This can e.g. be done with some cheap and widely available EPROM programmers like the TL866-II or the T48. The required JED files can be found in the Files directory. 

### Disclaimer

> [!CAUTION]
>**USE AT YOUR OWN RISK.**
>
>This is a hobby project, I am a hobbyist and no engineer. There is always the risk that the expansion can cause harm to your CPC. 
>Although I have tested the expansion on several CPCs for many hours with many other expansions and lots of software, there is no guarantee that it will properly work under all circumstances, with all expansions or with all revisions of the CPC 464 / 664.
>
> Especially if you are building this for others (commercially or not) make sure to make your own intense tests to guarantee this expansion works as expected before handing over to the recipients.  
>
>**USE AT YOUR OWN RISK.** 

### Bill of Materials

> [!IMPORTANT]
> Mouser IDs not verfified yet. If someone had a list of all the component IDs from e.g. Mouser or Digikey, please share the list so I can add it here.
> 
> Mouser IDs are just examples. You can use any compatible component (same specs).

| Part | Mouser No. (example, not verified yet) | Quantity |
| --- | --- | --- |
| PCB (thickness: 1.2mm) | n/a | x1 |
| ATF16V8 | 556-AF16V8B15PU | x3 |
| 74HCT174 or 74LS174 | 595-CD74HCT174E | x1 |
| AS6C4008-55 <sup>*</sup> | 913-AS6C4008-55PIN | x2 |
| Capacitor 100nF 104 2.54mm | 581-AR155C104K4R | x6 |
| Capacitor 22uF - 2.0mm | e.g. 598-106SVF025M  | x1 |
| Resistor 10k or 4k7 | | x1 |
| IC socket 40pin | 737-ICS-640-T | x1 |
| optional (but recommended):<br>IC socket 32pin <sup>**</sup> | 737-ICS-632-T | x2 |
| optional (but recommended):<br>IC socket 20pin <sup>**</sup> | 737-ICS-320-T | x3 |
| optional (but recommended):<br>IC socket 16pin | 737-ICS-316-T | x1 |
| Pin Header 1x20 | e.g. 200-TS120TAA (precise)| x2 |
| optional:<br>Pin Header 1x2 angled<br>or JST XH 2.5mm Pin male right angle| 538-90121-0122 <br>JST: 306-S2B-XH-ALFSN | x1 |

<sup>\*: AS6C4008 or compatible. If you are building the 576K version, only a single SRAM is needed. </sup>

Order List from Reichelt/Germany: https://www.reichelt.de/my/2256222 (list not verfified yet, please let me know if this works out for you).


> [!IMPORTANT]
> Make sure to buy all ICs in DIP format.
>
> 1x20 Pin Header: normal pin headers put some strain on the socket which could end in a socket that can no longer hold the plain CPU. Especially if you plan to remove the expansion again, make sure to use precise pin headers. However those break more easily, especially when not put into the socket gently and straight. 

<img src="/pictures/build1_rev2.jpeg" width="640"/>

1. PCB 
2. 2x SRAM AS6C4008 (DIP)
3. 74HCT174 or 74LS174
4. 3x ATF16V8 (DIP)
5. Resistor 10k or 4.7k
6. Cap 22uF, 2mm
7. 6x Cap 100nF 104 2.5mm
8. 2x Pin Header 1x20 (2.54mm)
9. IC Socket 40pin
10. 2x IC Socket 32pin
11. 3x IC Socket 20pin
12. IC Socket 16pin
13. Standoff (3D printed)

<sup>10-13: optional</sup>

### PCB

Order PCB here: https://www.pcbway.com/project/shareproject/CPC_iRAM_1024_1MB_internal_RAM_expansion_for_the_Amstrad_CPC_464_and_664_9310ac8d.html

or use the Gerber files from the files folder to order from your preferred PCB manufacturer. 

Recommended thickness is 1.2mm.

### Assembly

Preparations:

1) If you use normal pin headers (not recommended) instead of precise pin headers they usually need to be adjusted slightly as one side of the pin headers is too short and the other too long. You can move the plastic bar with e.g. pliers easily. Move them until the plastic bar almost reaches the mid of the pin header. One side should be slightly shorter than the other side. The short side will be the one that is later plugged into the CPU socket on the motherboard.

2) Program the ATF16V8 CPLDs with your programmer. Make sure to mark each one so you can later identify PAL1, PAL2 and PAL3.

**Step 1:**

On the bottom side of the PCB add the pin headers. 

<img src="/pictures/build2_rev2.jpeg" width="640"/>

> [!TIP]
> To easily align the pin headers you can insert them into the CPU socket before soldering. This keeps them nicely in place and aligned.

Cut the pins of the pin header on the top of the PCB closely to the PCBs surface.

**Step 2:**

On top add all remaining components. If you are not using sockets, solder all ICs first, then the CPU socket. If you are using sockets for all ICs, just solder all sockets. Resistor and capacitors come last.

<img src="/pictures/build3_rev2.jpeg" width="640"/>

If you want to be able to disable the iRAM manually you can solder a pin header to the DIS labeled connections and attach a switch to it which can be placed outside of the computer.

<sup>In case you are assembling the 576K version with a single SRAM you can leave out the sockets/ICs for PAL3 and SRAM2. However if you are using sockets it's recommended to fit them now for an easier, later upgrade.</sup> 

> [!IMPORTANT]
> Due to the tight packing of all components it's easy to accidentally add shorts or create a cold solder joint. Be careful when soldering and better check all connections twice. 

**Step 3:**

If you have been using sockets finally put the ICs into their respective sockets (except for CPU). 

### Variations

#### 1088K / 576K - no C3
Use the JED files with "no_C3" in the filename to program PAL 3. (PAL 1 ans PAL 2 will be identical for all variations.) 
If you only want to use a single SRAM, leave SRAM socket 2 empty. You can upgrade any time to 1088K later without further modifications. 

## Installation

Gently remove the CPU from its socket on the CPC motherboard.

<img src="/pictures/install1.jpg" width="640"/>

Insert it into the CPU socket on the expansion. 

<img src="/pictures/install2.jpg" width="640"/>

Now insert the expansion into the CPU socket on the motherboard. If any capacitors are blocking then gently bend them towards the motherboard until they no longer touch the expansion PCB. 

<img src="/pictures/install3.jpg" width="640"/>
 
Push the expansion into the socket until it sits tight. This usually needs a bit of force (GENTLY!) to properly snap in.

<img src="/pictures/installed464board1.jpg" width="640"/>

Turn on the CPC - and enjoy!

> [!NOTE]
> The CPCs boot message is hard coded in ROM so it will continue to show "64K". To test the expansion you can e.g. use the [Amstrad diagnostics](https://github.com/llopis/amstrad-diagnostics).

### CPC 464 - board revision 3 

If your CPC 464 has [motherboard revision 3](https://www.cpcwiki.eu/index.php/Mainboard_Versions#CPC464_version_3_.28medium-sized.29) (joystick port on the left) with Gate Array 40007 the cooling plate of the Gate Array blocks the installation of the iRAM 464. In this case you can bend the blocking edge slightly upwards to make it fit. 

<img src="/pictures/installed464board3.jpg" width="640"/>

### CPC 664

The board will fit into the CPC 664 without modifications.

<img src="/pictures/installed664.jpg" width="640"/>

## Thanks

Special thanks go to
- Revaldinho - [your solution](https://github.com/revaldinho/cpc_ram_expansion/wiki/Universal-Amstrad-CPC-RAM-Card) to implement C3 via shadowing on your external card inspired the C3 solution implemented here
- Prodatron - SymbOS is probably THE reason to have 1MB in a CPC 
