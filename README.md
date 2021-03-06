# Tenma DC power supply controllers

Provides two basic controllers (tested on Linux) for a TENMA DC power supply via serial interface.

 * tenmaControl (command line utility)
 * gtkIndicator (GTK indicator to sit on tray)

# tenmaControl

## What is this?

A small command line program / library to setup a Tenma 72-2540 DC POWER SUPPLY from your computer via SERIAL.

Coming back from holidays was hard. So I spent some time with a little game (tongue). You'll find a small explanation of the code in:

[https://jcastellssala.com/2017/10/31/tenma72-2540-linux-control/](https://jcastellssala.com/2017/10/31/tenma72-2540-linux-control/)

## Requirements

Python and the serial and click libraries:

	pip install pyserial
	pip install click

Shortcomings:

 * Cannot read current consumption. (Function implemented, does not seem to work)
 * Always saves to memory 1. (Function implemented, POWER SUPPLY not behaving as expected. Restores all memories correctly though.
 * The physical buttons are blocked for a while after connecting.
 * The safeON method does not select channels.
 * The safe current and voltage values are hardcoded in Tenma72_2540 class. To use different values, either overwrite them in tenmaDcLib.py, or use safeC and safeV cli args.


## Usage examples

### Print the Tenma version

	python tenmaControl.py /dev/ttyUSB0

### Set the current and the voltage

For example: 2.2 Amperes 5V:

	python tenmaControl.py -c 2200 -v 5000 /dev/ttyUSB0

### Turn on the channel output

	python tenmaControl.py --on /dev/ttyUSB0

### Turn OFF the channel output

	python tenmaControl.py --off /dev/ttyUSB0

### Load an existing memory

	python tenmaControl.py -r 1
	python tenmaControl.py --recall 2

### Create a new value for a memory 4

	python tenmaControl.py -c 2200 -v 5000 --save 4 /dev/ttyUSB0

### Print everything

	python tenmaControl.py -c 2200 -v 5000 --save 4 --verbose --debug /dev/ttyUSB0

# gtkIndicator

A very simple GTK indicator to control a tenma DC power supply from a graphical desktop. Provides ON, OFF and RESET facilities. Simply start it with:

	./gtkIndicator.py

### Safely turn on while checking current (3A) and voltage (12V) before turning on

    python tenmaControl.py --safeOn /dev/ttyUSB0

### Safely turn on while checking custom current (safeC=2000 mA) and voltage (safeV=5000 mV) before turning on

    python tenmaControl.py --safeOn --safeC 2000 --safeV 5000 /dev/ttyUSB0
