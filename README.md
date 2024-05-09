
[![Arduino CI](https://github.com/RobTillaart/LTR390_DFR/workflows/Arduino%20CI/badge.svg)](https://github.com/marketplace/actions/arduino_ci)
[![Arduino-lint](https://github.com/RobTillaart/LTR390_DFR/actions/workflows/arduino-lint.yml/badge.svg)](https://github.com/RobTillaart/LTR390_DFR/actions/workflows/arduino-lint.yml)
[![JSON check](https://github.com/RobTillaart/LTR390_DFR/actions/workflows/jsoncheck.yml/badge.svg)](https://github.com/RobTillaart/LTR390_DFR/actions/workflows/jsoncheck.yml)
[![GitHub issues](https://img.shields.io/github/issues/RobTillaart/LTR390_DFR.svg)](https://github.com/RobTillaart/LTR390_DFR/issues)

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/RobTillaart/LTR390_DFR/blob/master/LICENSE)
[![GitHub release](https://img.shields.io/github/release/RobTillaart/LTR390_DFR.svg?maxAge=3600)](https://github.com/RobTillaart/LTR390_DFR/releases)
[![PlatformIO Registry](https://badges.registry.platformio.org/packages/robtillaart/library/LTR390_DFR.svg)](https://registry.platformio.org/libraries/robtillaart/LTR390_DFR)


# LTR390_DFR

Arduino library for the I2C LTR390 UV sensor (DF Robotics edition).


## Description

Experimental

This library 

Operating voltage range: 3.0 - 5.0 V (tolerant).



## I2C

The device should work on 100 Khz and 400 Khz I2C bus.

Fixed address of 0x53 == 83 decimal according to datasheet.
However 0x1C / 28 was found with I2C scanner.


#### Multiplexing

Sometimes you need to control more devices than possible with the default
address range the device provides.
This is possible with an I2C multiplexer e.g. TCA9548 which creates up
to eight channels (think of it as I2C subnets) which can use the complete
address range of the device.

Drawback of using a multiplexer is that it takes more administration in
your code e.g. which device is on which channel.
This will slow down the access, which must be taken into account when
deciding which devices are on which channel.
Also note that switching between channels will slow down other devices
too if they are behind the multiplexer.

- https://github.com/RobTillaart/TCA9548



#### Related

- https://github.com/RobTillaart/LTR390_RT   (native LTR390)
- https://github.com/RobTillaart/LTR390_DFR  (DF Robotics variant)


## Interface   TODO elaborate...

```cpp
#include "LTR390_DFR.h"
```

#### Constructor

- **LTR390_DFR(TwoWire \* wire = &Wire)** 
- **bool begin()**
- **bool isConnected()** returns true if address is seen on I2C bus.
- **uint8_t getAddress()**


#### Main control

- **void setALSMode()**
- **void setUVSMode()**
- **void reset()**


#### Part and revision ID

- **uint8_t getPartID()** returns 11.
- **uint8_t getRevisionID()** returns 2.


#### Measurement configuration

- **void setResolution(uint8_t res)**  //  0..5
- **uint8_t getResolution()**
- **void setRate(uint8_t rate)**  //  0..7
- **uint8_t getRate()**
- **void setGain(uint8_t gain)**  //  0..4
- **uint8_t getGain()**



#### Main status

- **uint8_t getStatus()**  need split? or masks?

#### Get data

- **uint32_t getALSData()**
- **uint32_t getUVSData()**


#### Interrupt

- **int setInterruptConfig(uint8_t value)**
- **uint8_t getInterruptConfig()**
- **int setInterruptPersist(uint8_t value)**
- **uint8_t getInterruptPersist()**

#### Threshold

- **void setHighThreshold(uint32_t value)**
- **uint32_t getHighThreshold()**
- **void setLowThreshold(uint32_t value)**
- **uint32_t getLowThreshold()**


## Future

#### Must

- improve documentation
- test with hardware
- keep in sync with LTR390_RT when possible

#### Should

- add examples
- fix / elaborate TODO's
- test setGain()
- test setIntegrationTime()
- add setUVsensitivity()


#### Could

- add error handling
- unit test ==> test examples


#### Wont


## Support

If you appreciate my libraries, you can support the development and maintenance.
Improve the quality of the libraries by providing issues and Pull Requests, or
donate through PayPal or GitHub sponsors.

Thank you,


