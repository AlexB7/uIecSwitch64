# uIecSwitch
Written by Glenn Holmer (a.k.a "Shadow", a.k.a "Cenbe").

## Overview

uIecSwitch is a GEOS 64 application for switching between disk images on a uIEC or sd2iec drive.


## Compiling

The following libraries are required from the GOES 2.0 source code at https://github.com/mist64/geos/tree/master/inc

	geosmac.inc
	geossym.inc
	jumptab.inc

The button bitmap data is contained inside the main source file uIecSwitch128.S.  If the .png/.pcx source images are changed, they need to be recompiled using sp65 and then manually added to uIecSwitch128.S.  If needed, use Gimp to convert from .png to .pcx.

	sp65 -v -r button-open.pcx -c geos-bitmap -w button-open.s,format=asm
	sp65 -v -r button-parent.pcx -c geos-bitmap -w button-parent.s,format=asm
	sp65 -v -r button-up.pcx -c geos-bitmap -w button-up.s,format=asm
	sp65 -v -r button-down.pcx -c geos-bitmap -w button-down.s,format=asm

The program icon is contained in icon-program.bin.  If the .png/.pcx source image is changed, it needs to be recompiled using sp65.

	sp65 -v -r icon-program.pcx -c geos-icon -w icon-program.bin,format=bin

The following will compile, resulting in a regular program file which can then be converted using Convert in GEOS.

	ca65 -t geos-cbm uIecSwitchS.s
	grc65 -t geos-cbm uIecSwitchG.grc
	ca65 -t geos-cbm uIecSwitchG.s
	ld65 -t geos-cbm -o uIecSwitch.cvt uIecSwitchS.o uIecSwitchG.o geos-cbm.lib
