# SnappyROM
128KB ROM update for the Super Snapshot V5 Commodore 64 cartridge.

Compatible with the original SSv5, EasyFlash3[^1], Vice 3.6, Kung Fu Flash, 1541 Ultimate, Ultimate 64 and the still yet-to-be-released Snappy cartridge.

## New features
+ Turbo Macro PRO (TMP) is included in the ROM. 
+ JiffyDOS compatible loader.  Compatible with SD2IEC-type devices.
+ Wedge improvements:  @CD: can now be used in a directory listing.  It is mapped to the F6 key.
+ CodeNet support (currently requires a Snappy cartridge with a WiFi module).  Launched by typing @@C at the BASIC prompt.
+ The default start-up menu action is now to exit to BASIC (DEL exit instead of F7).

### New in V5.34
+ The wedge now moves the cursor down to an empty line before executing a
command.
+ Improved compatibility with JiffyDOS kernal, if present:
    * Using Ctrl-D to switch to the next available IEC device works as expected
    now.  Using >#n to switch devices with the Snapshot wedge now also updates
    JiffyDOS's active device.
    * SuperSnapshot Turbo load and save now fall back to kernal load/save if
    both a JD kernal and a JD-compatible drive are present.
+ Fixed compatibility with 16MB REUs (1541U, Ultimate 64).  A 16MB REU
would be reported as no REU being present because an overflow in the size
detect routine.
+ Fixed compatibility (hang at boot) with an ARMSID installed in the first 
socket of a SIDFX.

See the extended readme file for more details.

## Links
+ [CPLD upgrade for the EF3](https://github.com/adrianglz64/easyflash3-cpld)
+ [CPLD upgrade for the EF3 with FC3 support](https://github.com/adrianglz64/easyflash3-fc3)
+ [EF3 CPLD upgrade instructions](https://skoe.de/easyflash/ef3update/) (scroll down to CPLD CORE section)

[^1]: EF3 needs CPLD upgrade to support 128K SuperSnapshot ROMs
