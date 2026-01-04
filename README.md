# CPC464 iRAM/1024

> [!IMPORTANT]
>**An incompatibility with the M4 board has been reported. This PCB version will NOT work with the M4 without manual modifications.**
> See Issues for link to more details. 
>**Do not build this version if you are planning on using it with the M4.**
>
> At the moment the issue seems to be limited to M4 only but the root cause has not been identified yet.


<!--
> [!TIP]
> PCBs can be ordered at [PCBWay](https://www.pcbway.com/project/shareproject/CPC_iRAM_1024_1MB_internal_RAM_expansion_for_the_Amstrad_CPC_464_and_664_9310ac8d.html) with a few clicks. Recommended PCB thickness is 1.2mm.
-->

The iRAM/1024 is an internal RAM expansion for the Amstrad CPC 464 and CPC 664 which upgrades the computer to a total of 1024KB - sixteen times the amount of the original 64KB. 

It also support [C3 paging mode](http://norecess.cpcscene.net/advancedmemoryusage.html) which allows you to run CP/M plus, FutureOS or some games and demos with C3 requirement (e.g Pac-Man emulator or the demos PHX and Phortem).

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

- total of 1024K RAM (the primary config): 2x 512K SRAM, C3 support
- total of 640K RAM: 1x 512K SRAM + 1x 128K SRAM, total 640K RAM, C3 support
- total of 576K, 1x 512K SRAM, <b>no C3</b>

<sup>For the 640K version a small cut has to be made on the bottom of the PCB (clearly indicated) and a second resistor is required. For the 576K version you just need to close some bridges on the PCB and can save a few € as you only need 1 SRAM and 2 CPLD ICs.</sup>

(Personal comment: The 640K actually only makes sense if you have a 128K SRAM lying around. Otherwise the price difference between 512K and 128K is negligible.) 

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

- **An incompatibility with the M4 board has been reported.**
- In some CPC 464 (motherboard rev. 3 with GateArray 40007 fitted)the heat sink of the Gate Array might block the installation. The heat sink needs to be bent or replaced. See below for details.
- On beta tester reported crashes in BATMAN demo. These could be resolved with a different CPU. It has not been clear what has caused the issue. It might be due to lack of power through the CPU socket. If you experience the issue try cleaning the CPU socket and properly placing the iRAM into the socket to limit resistance. If this won't help replace the 22uF cap with a 47uF cap and/or connect the spare 5V/GND pins (bottom left side of the PCB) to a 5V and GND pin on the motherboard. Please reach out via "Issues" or the CPC Wiki if you experience the issue and share if/how you could solve it.
- Not really an issue but working as designed: the upper most 64K of the secondary SRAM are used for C3 emulation and are not available for applications or programs. Software therefore can access 64K base RAM + 960K expanded RAM (not 1024K). Properly designed software like SymbOS that tests the availability of RAM banks before using them will not be impacted but if software just assumes that a full 1024K of expansion RAM are present they might experience crashes once software accesses this RAM area. As that much RAM is only used by a few tech demos, FutureOS and SymbOS, the real world relevance is negligible, especially since SymbOS is limited to a total memory size of 1MB and won't be able to use the upper most 64K anyway. If there is demand for a full 1024K of expanded memory I can provide a JED to replace the third GAL chip which removes C3 support and enables access to the full 1024K of expanded RAM. 
  
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
| ATF16V8 <sup>**</sup> | 556-AF16V8B15PU | x3 |
| 74HCT174 or 74LS174 | 595-CD74HCT174E | x1 |
| AS6C4008-55 <sup>*</sup> | 913-AS6C4008-55PIN | x2 |
| Capacitor 100nF 104 2.54mm | 581-AR155C104K4R | x6 |
| Capacitor 22uF - 2.0mm | e.g. 598-106SVF025M  | x1 |
| Resistor 10k<sup>***</sup><br>(4k7 will also be fine) | | x1 |
| IC socket 40pin | 737-ICS-640-T | x1 |
| optional:<br>IC socket 32pin <sup>**</sup> | 737-ICS-632-T | x2 |
| optional:<br>IC socket 20pin <sup>**</sup> | 737-ICS-320-T | x3 |
| optional:<br>IC socket 16pin | 737-ICS-316-T | x1 |
| Pin Header 1x20 | e.g. 200-TS120TAA (precise)| x2 |
| optional:<br>Pin Header 1x2 angled<br>or JST XH 2.5mm Pin male right angle| 538-90121-0122 <br>JST: 306-S2B-XH-ALFSN | x1 |

<sup>\*: AS6C4008 or compatible. If you are building the 640K version, the second SRAM can be a AS6C1008 (or compatible). If you are building the 576K version, the second SRAM is not needed. </sup>

<sup>\**: If you are building the 576K version only 2x ATF16V8, 1x 32pin socket and 2x 20pin socket is required. However it's still recommended to populate the sockets to ensure an easy upgrade later.</sup>

<sup>\***: 2x resistor if you are building the 640K version</sup> 


Order List from Reichelt/Germany: https://www.reichelt.de/my/2256222 (list not verfified yet, please let me know if this works out for you).

List for 1024MB version. Please adjust the components if you plan to build the 640K or 576K version. 
​ 

> [!IMPORTANT]
> Make sure to buy all ICs in DIP format.
>
> 1x20 Pin Header: normal pin headers put some strain on the socket which could end in a socket that can no longer hold the plain CPU. Especially if you plan to remove the expansion again, make sure to use precise pin headers. However those break more easily, especially when not put into the socket gently and straight. 

<img src="/pictures/build1.jpg" width="640"/>

1. PCB 
2. 2x SRAM AS6C4008 (DIP)
3. 6x Cap 100nF 104 2.5mm
4. 3x ATF16V8 (DIP)
5. 74HCT174 or 74LS174
6. Resistor 10k or 4.7k
7. IC Socket 40pin
8. 2x Pin Header 1x20 (2.54mm)
9. Cap 22uF, 2mm

### PCB

Order PCB here: https://www.pcbway.com/project/shareproject/CPC_iRAM_1024_1MB_internal_RAM_expansion_for_the_Amstrad_CPC_464_and_664_9310ac8d.html

or use the Gerber files from the files folder to order from your preferred PCB manufacturer. 

Recommended thickness is 1.2mm.

### Assembly

Preparations:

1) If you use normal pin headers (not recommended) instead of precise pin headers they usually need to be adjusted slightly as one side of the pin headers is too short and the other too long. You can move the plastic bar with e.g. pliers easily. Move them until the plastic bar almost reaches the mid of the pin header. One side should be slightly shorter than the other side. The short side will be the one that is later plugged into the CPU socket on the motherboard.

2) Program the ATF16V8 CPLDs with your programmer. Make sure to mark each one so you can later identify PAL1, PAL2 and PAL3.

<sup>In case you are assembling the 576K version with a single SRAM you don't need PAL3.</sup> 

**Step 1:**

On the bottom side of the PCB add the pin header and the 10K resistor on the right hand side (picture update pending). 

<img src="/pictures/build2.jpg" width="640"/>

<sup>In case you are assembling the 640K version make sure to cut the trace at the indicated position and add the additional 10K resistor.</sup> 

<sup>In case you are assembling the 576K version with a single SRAM make sure to close all the L-bridges (L1 to L4).</sup>

> [!TIP]
> To easily align the pin headers you can insert them into the CPU socket before soldering. This keeps them nicely in place and aligned.

Cut the pins of the pin header on the top of the PCB closely to the PCBs surface.

**Step 2:**

On top add all remaining components. If you are not using sockets, solder all ICs first, then the CPU socket. If you are using sockets for all ICs, just solder all sockets. Capacitors come last.

<img src="/pictures/build3.jpg" width="640"/>

If you want to be able to disable the iRAM manually you can solder a pin header to the DIS labeled connections and attach a switch to it which can be placed outside of the computer.

<sup>In case you are assembling the 576K version with a single SRAM you can leave out the sockets/ICs for PAL3 and SRAM2. However if you are using sockets it's recommended to fit them now for an easier, later upgrade.</sup> 

> [!IMPORTANT]
> Due to the tight packing of all components it's easy to accidentally add shorts or create a cold solder joint. Be careful when soldering and better check all connections twice. 

**Step 3:**

If you have been using sockets not put the new ICs into their respective sockets (except for CPU). 

### Variations

#### 640K - SRAM 512k + SRAM 128k
If you install a 128K SRAM in the lower SRAM slot you need to cut the bridge (1) and add a 10k or 4.7k resistor (2) on the backside of the PCB. The iRAM will then provide 640K of total RAM incl. C3 support. 
<img src="/pictures/variation640k.jpg" width="640"/>

#### 576K - SRAM 512k
If you install only a single 512k SRAM in the upper SRAM slot and leave the lower SRAM empty you need to close all LK bridges on the backside of the PCB. The iRAM will then provide a total of 576k of RAM *without* C3 support. 

<img src="/pictures/variation576k.jpg" width="640"/>

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
