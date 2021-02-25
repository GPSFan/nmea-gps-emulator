# NMEA-GPS Emulator

[![Python 3.8.5](https://img.shields.io/badge/python-3.8.5-blue.svg)](https://www.python.org/downloads/release/python-385/)
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)

The **NMEA-GPS Emulator** is a simple script that emulates a GPS receiver (simulates unit's movement). Data generated by the script are sent to clients in **NMEA 0183** format. 
This script can be useful for testing applications or systems that require some unit's GPS position data.

The **NMEA-GPS Emulator** script can be used in one of the following operating modes:
- NMEA TCP Stream (sends TCP packets to the specified client),
- NMEA UDP Stream (sends UDP packets to the specified client),
- NMEA TCP Server (the server waits for client connections, then sends TCP packets to the connected clients - max 10 connections)
- NMEA Serial (transmit serial data on specified RS port).
***
## Features
The script allows the user to enter the following data:
- unit's position;
- unit's speed;
- unit's course;
- operating mode selection (NMEA Serial, NMEA TCP Server, NMEA TCP or UDP Stream);
- pair ip address and port or serial port name.

After selecting one of the operating modes, the script allows the user to interactively change the speed and course of the unit.

List of NMEA sentences generated by **NMEA-GPS Emulator** script:
```
GPGGA - Global Positioning System Fix Data
GPGLL - Position data: position fix, time of position fix, and status
GPRMC - Recommended minimum specific GPS/Transit data
GPGSA - GPS DOP and active satellites
GPGSV - GPS Satellites in view
GPHDT - Heading, True.
```
Output example:
```
$GPGGA,065835.00,5430.000,N,01920.144,E,1,04,0.92,15.2,M,32.5,M,,*65
$GPGSA,A,3,10,22,20,14,,,,,,,,,1.56,0.92,1.25*0B
$GPGSV,4,1,15,12,59,132,28,08,84,226,64,13,90,018,80,15,40,355,37*70
$GPGSV,4,2,15,30,38,303,41,16,35,337,85,09,13,089,00,20,29,100,16*78
$GPGSV,4,3,15,10,55,159,60,14,39,062,32,22,83,011,98,17,44,213,18*7F
$GPGSV,4,4,15,06,25,203,12,32,49,082,77,02,24,005,46*4B
$GPGLL,5430.000,N,01920.144,E,065835.000,A,A*5D
$GPRMC,065835.000,A,5430.000,N,01920.144,E,10.500,90.0,150221,,,A*62
$GPHDT,90.0,T*0C
$GPZDA,065835.000,15,02,2021,0,0*5C
```

***
## Getting Started

Below instructions will get you a copy of the project up and running on your local machine.

### Requirements

Python third party packages:
* [pyproj](https://pypi.org/project/pyproj/)
* [pyserial](https://pypi.org/project/pyserial/)
* [psutil](https://pypi.org/project/psutil/)

In order to use **NMEA Serial** mode correctly, it is necessary to use dedicated serial **null modem** cable.

On Linux systems you will probably need to change the permissions for the device matching your serial port before running the script.
```bash
# Example command for /dev/ttyUSB0 device
sudo chmod a+rw /dev/ttyUSB0
```

### Installation with venv
The script can be build and run locally with virtualenv tool. Run following commands in order to create virtual environment and install the required packages.
```bash
$ virtualenv venv
$ source venv/bin/activate
(venv) $ pip install -r requirements.txt
```
### Running the script
You can start the script using the following command:
```bash
(venv) $ python main.py
```
After starting the script correctly, the following prompt should appear in the OS console:

```bash
.##..##..##...##..######...####...........######..##...##..##..##..##.......####...######...####...#####..
.###.##..###.###..##......##..##..........##......###.###..##..##..##......##..##....##....##..##..##..##.
.##.###..##.#.##..####....######..........####....##.#.##..##..##..##......######....##....##..##..#####..
.##..##..##...##..##......##..##..........##......##...##..##..##..##......##..##....##....##..##..##..##.
.##..##..##...##..######..##..##..........######..##...##...####...######..##..##....##.....####...##..##.
..........................................................................................................


### Choose emulator option: ###
1 - NMEA Serial
2 - NMEA TCP Server
3 - NMEA TCP or UDP Stream
### "Ctrl + c" for exit ###
>>> 

```