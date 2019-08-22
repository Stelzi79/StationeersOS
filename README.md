# StationeersOS

A ship/station/base operating system entirely constructed from programmable logic/IC chip in the game [Stationeers](http:www.stationeers.com).

Stationeers is a space survival game that lets you engineer intricate systems to construct a space ship, space station or a base on a moon or planet. It also has a complex system of logic chips and programmable [IC chips](https://stationeers-wiki.com/Integrated_Circuit_(IC10)) to automate and every process.

This project attempts to form with many of these chips an interconnected operating system that lets you operate your ship/station/base like one unit.

It manly consists (at this time) of many [IC10 chips](https://stationeers-wiki.com/Integrated_Circuit_(IC10)) that have the following capabilities:

* 6 + 1 IO pins (d0 - d5 and device base)
* 17 registers (r0 - r15, sp, ra)
* MIPS based and turing complete instruction set
* 128 instructions/lines per IC10
* 512 stack space

6 GPIOs and 128 lines of programming space is the limiting factor of having game wide automatisation and display.
