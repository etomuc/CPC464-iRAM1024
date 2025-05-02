# CPC464 iRAM/1024

The iRAM/1024 is an internal RAM expansion for the Amstrad CPC 464 and CPC 664 which upgrades the computer to a total of 1024KB - sixteen times the amount of the original 64KB. 

It also support [C3 paging mode](http://norecess.cpcscene.net/advancedmemoryusage.html) which allows you to run CP/M plus, FutureOS or some games and demos with C3 requirement (e.g Pac-Man emulator or the demos PHX and Phortem).

<img src="/pictures/Iram1024_builtin.jpg" width="640"/>

Legacy software that supports the DK'Tronics memory standard will be able to access up to 576K of RAM ([the maximum suppored by DK'Tronics](https://www.cpcwiki.eu/index.php/Standard_Memory_Expansions#Standard_128K-512K_Expansions_.28dk.27tronics.2Fdobbertin-style.29)). More recent software, like e.g. SymbOS, with support for the [enhanced Yarek/RAM7 standard](https://www.cpcwiki.eu/index.php/Standard_Memory_Expansions#Extended_1M-4M_Expansions_.28RAM7.2FYarek-style.29) will see the full 1024K. 

## Variations

The same PCB supports 3 RAM configurations: 

- total of 1024K RAM (the primary config): 2x 512K SRAM, C3 support
- total of 640K RAM: 1x 512K SRAM + 1x 128K SRAM, total 640K RAM, C3 support
- total of 576K, 1x 512K SRAM, <b>no C3</b>

<sup>For the 640K version a small cut has to be made on the bottom of the PCB (clearly indicated) and another resistor is required. For the 576K version you just need to close some bridges on the PCB and can save a few € as you only need 1 SRAM and 2 CPLD ICs.</sup>

(Personal comment: The 640K actually only makes sense if you have a 128K SRAM lying around. The price difference if you buy new is negligible.) 

## Goals

Main goals of this expansions were:
- fits into a standard CPC 464 and 664
- full CPC 6128 compatibility ([C3 paging mode](http://norecess.cpcscene.net/advancedmemoryusage.html)) to support CP/M plus, Future-OS and games/demos with C3 requirement.  
- requires no internal modifications, especially no additional internal soldering
- DIY friendly
	- all easy-to solder through-hole components
	- no FPGA, CPLDs can be programmed with many cheap EPROM programmers
- cheap - all components should be available for €20 or less
- long-term availability - all components are still manufactured and will probably be available for decades (at least as NOS)

## License

The expansion and all resources are free to use for personal use.

It is released under the CC BY-NC-ND 4.0 license with the following exception: Commercial production and selling is permitted (and encouraged) as long as the final product will be sold for a maximum of USD 40 / €40 / £38 or the equivalent in other currencies (excl. shipping and platform fees like e.g. for Ebay or SellMyRetro). 
<sub>Considering the cost of the components (especially when bought in quantities) and the time required for the assembly, this should be sufficient for an interesting profit margin while keeping the expansion affordable for the community.</sub> 

## Support

There is no official support. If you have any questions feel free to join the "Technical support - Hardware related" board on the cpcwiki.eu forum.

## Building the expansion

For a full assembly you need 
- basic soldering skills - as long as you can solder normal through hole components reliably, you will be fine.
- an option to program ATF16V8 CPLDs. This can e.g. be done with some cheap and widely available EPROM programmers like the TL866-II or the T48. The required JED files can be found in the Files directory. 

### Disclaimer

> [!CAUTION]
>**USE AT YOUR OWN RISK.**
>
>This is a hobby project, I am a hobbyist and no engineer. There is always the risk that the expansion can cause harm to your CPC. 
>Although I have tested the expansion on several CPCs for many hours with many other expansions and lots of software, there is no guarantee that it will properly work under all circumstances, with all expansions or with all revisions of the CPC 6128.
>
> Especially if you are building this for others (commercially or not) make sure to make your own intense tests to guarentee this expansion works as expected before handing over to the recipients.  
>
>**USE AT YOUR OWN RISK.** 

### Bill of Materials

> [!IMPORTANT]
> Mouser IDs not verfified yet. If someone had a list of all the component IDs from e.g. Mouser or Digikey, please share the list so I can add it here.
> 
> Mouser IDs are just examples. You can use any compatible component (same specs).

| Part | Mouser No. (example, not verified yet) | Quantity |
| --- | --- | --- |
| PCB | n/a | x1 |
| ATF16V8 | 556-AF16V8B15PU | x3 |
| 74HCT174 or 74LS174 | 595-CD74HCT174E | x1 |
| AS6C4008-55 (*) | 913-AS6C4008-55PIN | x2 |
| Capacitor 100nF 104 2.56mm | 581-AR155C104K4R | x5 |
| Capacitor 10uF (or 22uF) - 2.0mm | e.g. 598-106SVF025M  | x1 |
| Resistor 4.7k | | x1 |
| IC socket 40pin | 571-1-2199299-5 | x1 |
| Pin Header 1x20 | e.g. 517-2320-6121 (normal)<br>or  200-TS120TAA (precise)| x2 |
| optional:<br>Pin Header 1x2 angled<br>or JST XH 2.5mm Pin male right angle| 538-90121-0122 <br>JST: 306-S2B-XH-ALFSN | x1 |

<sup>*: AS6C4008 or compatible. If you are building the 640K version, the second SRAM can be a AS6C1008 (or compatible)</sup>

TODO: add ic sockets


Order List from Reichelt/Germany: https://www.reichelt.de/my/2247546 (list not verfified yet, please let me know if this works out for you).

List is for 6128 version. Please adjust the number of components to match the required amount. 
​ 

> [!IMPORTANT]
> Make sure to buy all ICs in DIP format.
>
> 1x20 Pin Header: normal pin headers put some strain on the socket. Especially if you plan to remove the expansion again, consider the precise pin headers. However those break easily when not put into the socket gently and perfectly aligned. 

<img src="/pictures/bom.jpg" width="640"/>


### PCB

TODO: Update
Order PCB here: https://www.pcbway.com/project/shareproject/CPC_iRAM640_internal_RAM_expansion_for_the_Amstrad_CPC_6128_5a46d826.html

or use the Gerber files from the files folder to order from your preferred PCB manufacturer. 

### Assembly

Preparations:

1) Some pin headers need to be adjusted slightly as usually one side of the pin headers is too short and the other too long. You can move the plastic bar with e.g. pliers easily. Move them until the plastic bar almost reaches the mid of the pin header. One side should be slightly shorter than the other side. The short side will be the one that is later plugged into the CPU socket on the motherboard.

2) Program the ATF16V8 CPLDs with your programmer. Make sure to mark each one so you can later identify PAL1, PAL2 and PAL3.

<sup>In case you are assembling the 576K version with a single SRAM you don't need PAL3.</sup> 

**Step 1:**

Add the resistor on the bottom side of the PCB. 

<img src="/pictures/assembly1.jpg" width="640"/>

<sup>In case you are assembling the 640K version make sure to cut the trace at the indicated position and add the additional 10K resistor.</sup> 

> [!TIP]
> To easily align the pin headers you can insert them into the CPU socket before soldering. This keeps them nicely in place and aligned.

Cut the pins of the pin header on the top of the PCB closely to the PCBs surface.

**Step 2:**

Solder all IC sockets on top of the PCB.

<img src="/pictures/assembly2.jpg" width="640"/>

<sup>In case you are assembling the 576K version with a single SRAM you can leave out the sockets for PAL3 and SRAM2. However it's recommended to fit them now for an easier, later upgrade.</sup> 

**Step 3:**

Solder the remaining components on top of the PCB. 

<img src="/pictures/assembly3.jpg" width="640"/>

<sup>In case you are assembling the 576K version with a single SRAM make sure to close all the L-bridges (L1 to L4).</sup> 

> [!IMPORTANT]
> Due to the tight packing of all components it's easy to accidentally add shorts or create a cold solder joint. Be careful when soldering and better check all connections twice. 

**Step 4:**

Put the new ICs into their respective sockets. 

**Step 5:**

Gently remove the CPU from its socket on the CPC motherboard and insert it into the CPU socket on the expansion. Now insert the expansion into the CPU socket on the motherboard (also gently, but usually needs a bit of force to properly snap into the socket).

Turn on the CPC - and enjoy!

> [!NOTE]
> The CPCs boot message is hard coded in ROM so it will continue to show "64K". To test the expansion you can e.g. use the [Amstrad diagnostics](https://github.com/llopis/amstrad-diagnostics).

## Variations


## Thanks

Special thanks go to
- Bryce - your willingness to share your knowledge with the community was a great help - without it I would have never even considered doing any electronics. I learned so much! 
- Bread80 - without your [documentation of the RAM logic in the CPC](https://bread80.com/2021/06/03/understanding-the-amstrad-cpc-video-ram-and-gate-array-subsystem/), this would not have been possible
- Prodatron - thanks a lot for your support and providing the source code that allowed me to find the RAM banking issue. (And your [SymbOS](http://www.symbos.de/) is the best reason to get 640K anyway)
- Toto - for your encouraging messages and your ideas and support
- the generous Ebay buyers of the first 4 final expansions - your purchase helped a lot to refinance the development costs of this expansion. (for anyone wondering: the initial 4 items will be the only ones ever sold by me and they came with a special certificate of authenticity - only those are legit first batch items)
