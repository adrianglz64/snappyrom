
======================================================
 SnappyROM V5.31/Style
======================================================
 128KB ROM update for the Super Snapshot V5 cartridge 
======================================================


Quick Start / TLDR
==================

SnappyROM is an updated ROM for your SuperSnapshot V5.  Burn it to a 128KB or 
bigger EPROM/FlashROM and use it to replace the EPROM in your SSv5.  It is also
compatible with the EasyFlash3, but a CPLD upgrade is needed to add 128K
compatibility.  Read on for more details.


Introduction
============

The Super Snapshot V5 freezer/utility cartridge was released sometime in early
1990.  It featured 64KB of ROM and 8KB of RAM.  The ROM included many useful
features such as fast load and save routines for 1541/71/81 drives, a file
copier, disk copier, and of course, a freezer that allowed you to save the
current program in memory to disk.  Several other utilities and monitors were
included.   The last version of the ROM that was released was V5.22.

SnappyROM is the result of disassembling and analyzing large parts of the
original V5.22 ROM in order to make improvements and add new features. It was
originally intended for use with my own SSv5-compatible cartridge ("Snappy"),
which includes a built-in REU and a bigger ROM, but I decided to keep everything
compatible with the original hardware for as long as possible.


New features
============

+ Turbo Macro PRO (TMP) is included in the ROM.  The start-up menu has been
modified to launch TMP with the F5 key.  The extended life feature that was
previously selected with F5 was moved to F6.  Both the standard and the REU 
versions of TMP are included.  If an REU is detected, the REU version of TMP 
will be loaded.

+ JiffyDOS compatible loader.  The original SuperSnapshot V5 Turbo DOS does not
work with 1541 drives that have a JiffyDOS ROM, and Turbo DOS is not compatible
with newer mass-storage devices like the SD2IEC and variants and reverts to slow
loading from them.  The updated loader fixes both of these problems.  Please see
the section "JiffyDOS Notes" for more on Jiffy load.

+ Wedge improvements:  @CD: can now be used in a directory listing and works
as expected.  It is also mapped to the F6 key when function keys are enabled
(F6 was previously mapped as a delete-equivalent key).

+ CodeNet support.  This feature currently requires a Snappy cartridge with a
WiFi module, but it might be updated to support cartridges like the 64Nic+ if
there is enough interest.  CodeNet is launched by typing @@C at the BASIC
prompt.

+ The default action when the start-up menu times out is now exiting to BASIC
without trying to boot the disk in the drive (like pressing DEL instead of F7).


Compatibility
=============

The original SSv5 cartridge fully supports 128K of ROM.  It was shipped with a
28-pin 64KB EPROM installed in a 32-pin socket, but everything was designed and
wired to support a 128KB ROM.  This was likely done to allow for future upgrades
that would require additional space, but no such ROM was ever released.  The
larger 32-pin socket allows for using 128KB, 256KB, and 512KB ROM chips
(although only 128KB is addressable).  The unused address pins are wired to Vcc.

To use SnappyROM you need to burn it to an EPROM or FlashROM and use that to
replace the ROM in your SSv5.  You can also run it on the Vice C64 emulator 
version 3.6 or newer.  Support for 128K SSv5 ROMs was added starting with SVN 
revision 39834.

To replace the ROM in your SSv5 you will need a 128KB, 256KB or 512KB EPROM or
FlashROM chip and an EPROM programmer.   Access times in the 100nS to 200nS
range are recommended.

The following is a list of EPROM and FlashROM chips that have been tested and
confirmed working with the original SSv5 hardware.  All of these chips were
acquired from various vendors on ebay in 2021.  They are not particularly hard
to find:


Part number     Size        Type    Speed   Result
--------------------------------------------------
AM27C010-120DC  128KB x 8 EPROM 120nS   OK
AT29C010A-12PC  128KB x 8 Flash 120nS   OK

AM28F020-200PC  256KB x 8 Flash 200nS   OK

AM27C040-150    512KB x 8 EPROM 150nS   OK
ST27C4001-10F1  512KB x 8 EPROM 100nS   OK

FlashROM chips are recommended because you don't need a UV lamp to erase them, 
but they are usually slighly more expensive than their EPROM counterparts.  If 
you do get a FlashROM chip, make sure it is supported by your EPROM programmer.

When using chips larger than 128K you can either write as many copies of the ROM 
as are necessary to fill your chip, or just burn it to the upper 128K of the 
chip.


Examples:
---------

* Concatenate two copies of the ROM to fill a 256KB chip:
    + DOS/Windows:  
        copy /b snappyrom.bin + snappyrom.bin snappyrom256.bin

    + Unix/Mac:
        cat snappyrom.bin snappyrom.bin >snappyrom256.bin


* Load the ROM into the upper 128K of the chip:
    + Using your EPROM programmer software, fill your buffer with 0xff and then
        - for a 256KB chip, load the ROM binary at hex 0x020000
        - for a 512KB chip, load the ROM binary at hex 0x060000


Replacing the ROM
-----------------

The original cartridge does not have any screws holding it together.  It is held
together merely by some plastic pins in the bottom half of the case that go into
holes in the top half of the case.  It is also held by the label that was
applied across the top and bottom halves.  Unfortunately, the label has to be
peeled from the back of the cartridge (the side facing away from your c64 when
the cartridge is inserted) in order to open it.

As mentioned previously, the original hardware has a 32-pin socket that
accommodates the larger 128KB, 256KB and 512KB chips, but the top half of the
cartridge case has a peg/cylinder in the middle that prevents it from closing
when using a 32-pin chip.  This plastic bit has to be filed down or cut if you
want to be able to close your case normally.  Note the orientation of the notch
on the EPROM before you remove it.  The notch has to face the card-edge (c64)
side.

If you decide to go back to your original 28-pin 64KB ROM chip (why would you
ever want to do that?), make sure you align the ROM with the RAM chip on the
right, leaving the 4 pins closest to the card-edge (c64) connector empty (two
empty pins on the left, two on the right).


EasyFlash 3 Notes
=================

The CPLD core on the EF3 can be updated using a PC/Mac/Linux connected to the 
EF3 via the mini-USB connector on the cartridge.  For details please visit:
https://skoe.de/easyflash/ef3update/

Look for the section "How to update the EasyFlash3 CPLD Core" near the end of 
the page.

The updated CPLD core can be downloaded from the links at the end of this
document.


JiffyDOS Notes
==============

This ROM includes a loader that is based on the loader in the JiffyDOS 6.0 ROM.
Please note that this is not intended as a replacement for JiffyDOS, and does
not offer the same level of compatibility that a real JiffyDOS replacement
Kernal ROM does.  The loader has been integrated into SuperSnapshot Turbo DOS,
so it is only active when Turbo DOS is active.  The loader does not include the
drive side of the code, so it will only work with devices that have a JiffyDOS
ROM, or devices like SD2IEC variants that natively support JiffyDOS.

JiffyDOS is a commercial product that is under copyright and can still be
purchased legally.  The Jiffy load feature is meant to be used in cases where
it's not practical to insall a Kernal ROM replacement in your c64/128.  If you
use it please consider purchasing an official Kernal ROM overlay IC or a ROM
image at:

https://store.go4retro.com/jiffydos-kernal-rom-overlay-ic/
https://store.go4retro.com/jiffydos-64-kernal-rom-overlay-image/

Please support the people still developing hardware and software for your C64!


Super Snapshot V5 Notes
=======================

Super Snapshot V5 is technically still in production using the same design
introduced in 1990, but actually buying a new one is next to impossible at the
time.  The rights are owned by Joe Palumbo, but the domain for his website has
expired, and he does not seem to answer emails often.

There are a few alternatives to an original cartridge:

+ The Easy Flash 3 cartridge supports 64KB SSv5 ROMs, but the CPLD can be
  upgraded to add 128K ROM support
+ Cartridges like the 1541 Ultimate can emulate a SSv5
+ SSv5 Clone (see links at the end)


Credits
=======

Code:
            dW/Style

Turbo Macro Pro:
            Elwix/Style and MO/Style

Special thanks to:

- jbevren for extensive Snappy hardware testing and analysis!
- Elwix/Style for lots of ideas and discussion.
- Six/Style for testing and actually using my cartridges all the time for years.
- TheFatman, Macbeth/PSW, JCompton for ROM testing and ideas.
- Groepaz and the Vice Team for their awesome emulator and for adding 128K 
  Snapshot ROM support to it.
- C0untZ3r0 for exchanging ideas and comparing notes on ROM development.
- BHZ/FTA and Dokken/Electron for constantly reminding me how they like 
  Action Replay a lot more than Super Snapshot.


Links
=====

+ Revision of Vice where support for 128KB SSv5 ROM was added
    https://sourceforge.net/p/vice-emu/code/39834/

+ SuperSnapshot V5 clone:
    https://github.com/Kalidomra/SuperClone-5.0

+ Retro Innovations JiffyDOS page
    https://www.go4retro.com/products/jiffydos/

+ CPLD upgrade for EF3 with 128K SSv5 ROM support:
	  https://github.com/adrianglz64/easyflash3-cpld

+ CPLD upgrade for EF3 with 128K SSv5 ROM and Final Cartridge 3 support:
		https://github.com/adrianglz64/easyflash3-fc3
