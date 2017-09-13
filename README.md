Universal MML Compiler & Music Driver
=====================================

_Nothing has been done yet, so far this is just a placeholder idea!!_

The goal of this project is to provide an MML and music driver that is sound chip and platform agnostic. That is to say that you write your music once, compile, and then play on a variety of systems with a variety of sound chips! (Which isn't to say that you can't customize your music to make use of different features depending on what's available when it's played.)

The compiler is written in Scheme and produces universal `.m` files given `.mml` files. There are many implementations of the music driver and player for various platforms, including a pseudo-player which outputs to  `.vgm` files. The players are simple programs which wrap their corresponding music driver library. Most players and libraries are written in platform-specific assembly, but the rest are written in Rust. The music driver libraries take music data (in the `.m` files) and convert it into commands for whichever sound chips are said to be available (which is a fixed set for many platforms, such as Game Boy, NES, etc., but is configurable, for example, when outputting to `.vgm`).

In addition there are drivers for accessing sound chips directly from your PC! Along with a corresponding music driver and player, as well as a `.vgm` player.

## Directories

`music_drivers` contains platform specific library implementations of the music driver.
`music_players` contains platform specific players which wrap their corresponding music driver libraries. (Includes the pseudo-player which outputs to `.vgm`.)
`mml_compiler` contains the MML compiler itself.
`sound_chip_drivers` contains drivers for interfacing sound chips directly from your PC.
`vgm_player` contains a `.vgm` player program that interfaces with sound chips connected directly to your PC.
`examples` includes example music projects written in MML.

## Compiling and Installing

`make` will compile the MML compiler, the music driver for PC, the sound chip drivers, the music player for PC, the pseudo player that outputs to `.vgm`, and the vgm player.
`make install` will copy the MML compiler, the music player, the `.vgm` player, and the `.vgm` generator to `/usr/local/bin/`.

To compile a music driver and player for a specific platform, type `make` followed by the platform:
`make gb` will compile the driver and player for Game Boy.
`make gba` will compile the driver and player for Game Boy Advance.
`make famicom` will compile the driver and player for Famicom.
`make zx` will compile the driver and player for ZX Spectrum.
`make c64` will compile the driver and player for Commodore 64.

Note that additional compilers and/or assemblers will be needed for each of these target platforms.

## Simple Usage

`mml2m tune.mml > tune.m` will compile `tune.mml` file into `tune.m` file.
`mplay tune.m` will play `tune.m` on whichever real sound chip hardware is attached to your PC.
`m2vgm tune.m sid > tune.vgm` will take `tune.m` and output `tune.vgm` file for the SID chip. If no sound chips are provided then it will default to the prefered sound chips as specified by the `.m` file (in turn specified in the original `.mml` file).
`vgmplay tune.vgm` will play `tune.vgm` on real sound chip hardware attached to your PC.

I'd suggest creating a Makefile for your music project containing these commands for easy access. For example: `make compile`, `make play`, and `make vgm`.

## MML and Music Format Specification

I'll put more info here later!!
