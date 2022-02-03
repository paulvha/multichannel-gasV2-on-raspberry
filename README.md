# Multichannel Gas Sensor V2 on RPI

## Background

Back 2017 I worked on a Grove MultiChannel board for the Raspberry Pi which included the mics6814. The findings and code can be found [here](https://github.com/paulvha/multichannel-gas)
After spending many hours analyzing I came to the conclusion :

*As a result I have spend much more time analyzing the board and software than I originally planned to do.
I have discovered a number of issues with the board to makes me question the measurement results and why this has not been detected before.*

I have left it for what is was.

Recently I was contacted by Frederic, who used the earlier work, about a [Grove - Multichannel gas sensor V2](https://wiki.seeedstudio.com/Grove-Multichannel-Gas-Sensor-V2/). Whether I had done RPI code on this ? I had not..
I decided to take a look at the information and the source code for an Arduino that is available.

The board has 4 MEMS sensors which are sensitive to different gasses: Carbon monoxide (CO), Nitrogen dioxide (NO2), Ethyl alcohol(C2H5CH), Volatile Organic Compounds (VOC). The sensors look to have good specifications and each can measure other gasses that are close to their sensativety. These sensors are connected to an board processor (STM32F030) and the I2C communication is handled with that processor. I find the board expensive (prices between 40 and 50 Euro), so I have high expectations.

There is a single channel and you can not address each sensor separately. The interface protocol is very basic, but nowhere I was able to find documentation. Only by studying the source code for the Arduino I found a few commands : start / stop preheating and get an ADC measurement from either sensor.

* What that ADC measurement means ? I don't know.
* How to use that measurement to determine the other gasses in the charts ? I don't know
* Are there more commands to set or influence the results? I don't know
* When is preheating necessary, for how long before, for which measurements ? I don't know
* Are the sensors or software calibrated or do the need burn in time ? I don't know
* The datasheets on the wiki website are in chinese. Not very helpfull.

Seems I am not alone, looking this [post](https://forum.seeedstudio.com/t/grove-multichannel-gas-sensor-v2-calibration/253136/13) are on the forum.

I had lost interest into this board given the very little amount of information, the limited protocol.
Still wanted to help Frederic and as we could not find code for the RPI on Github and other places, I decided to re-use part of my the earlier work and build a library and user level program. Frederic did the testing as he has a board.

I needed some challenge and there are actually 2 versions attached : one written in 'C' and the otherone written in 'C++". Functionally they do exactly the same, it is just what you prefer to use or maybe integrate with other code.

In the extras folder is a copy of the schema the board and for some sensors the english version.

## Prerequisites
[BCM2835 library](http://www.airspayce.com/mikem/bcm2835/)

## Installation instructions

Make your self superuser : sudo bash

### BCM2835 library Install latest from BCM2835 from : http://www.airspayce.com/mikem/bcm2835/

    cd /home/pi
    wget http://www.airspayce.com/mikem/bcm2835/bcm2835-1.68.tar.gz
    tar -zxf bcm2835-1.68.tar.gz // 1.68 was version number at the time of writing
    cd bcm2835-1.68
    ./configure
    sudo make check
    sudo make install

### C-Version
    Install the gass utility and library:

    cd /home/pi
    tar -xzvf MgassV2.tar.gz
    cd MgassV2
    ./mgass.sh

    To run the software you MUST be root/super user given the Linux permission: sudo ./gass2

    To get help : ./gass2-h

### C++ -version
    Install the gass utility and library:

    cd /home/pi
    tar -xzvf MgassV2++.tar.gz
    cd MgassV2++
    ./mgass.sh

    To run the software you MUST be root/super user given the Linux permission: sudo ./gass2

    To get help : ./gass2 -h

## Versioning

### version 1.1 / January 2022 / paulvha
* Initial release

## Author
 * Paul van Haastrecht (paulvha@hotmail.com)

## License
Parts of the library code is taken from SEEED Arduino library and is licensed under the MIT.
The user program is licensed under GNU-3

## Acknowledgements
Frederic in Switserland for collaboration and testing
