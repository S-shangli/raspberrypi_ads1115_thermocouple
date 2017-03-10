# raspberrypi_ads1115_thermocouple
Shellscript for the type-K thermocouple with ADS1115 on RaspberryPi.

# setting
|item|description|
|---|---|
|I2C_BUS=1|I2C bus number|
|ADS_ADDR="0x48"|ADS1115 I2C address|
|ADS_CONF_H_THERMO="0x8f"|settings of ADS1115 AD convert for typeK thermocouple|
|ADS_CONF_L_THERMO="0x03"|settings of ADS1115 AD convert for typeK thermocouple|
|ADS_CONF_H_LM61="0xe5"|settings of ADS1115 AD convert for LM61CIZ|
|ADS_CONF_L_LM61="0x03"|settings of ADS1115 AD convert for LM61CIZ|
|LSB_THERMO=7.8125|LSB voltage for typeK thermocouple|
|LSB_LM61=62.5|LSB voltage for LM61CIZ|

# usage
just execute. no need args.

    [pi@raspberrypi]% ./ads1115.sh
    Thermocouple_raw_HEX : 0008
    LM61CIZ_raw_HEX      : 2FC4
    Thermocouple_raw     : 8
    LM61CIZ_raw          : 12228
    Thermocouple_uV      : 62.5000 uV
    LM61_uV              : 764250.0 uV
    Thermocouple_degC    : 1.535626535626 degC
    LM61_degC            : 16.425000000000 degC
    RESULT : 17.960626535626 degC


# hardware list
* RaspberryPi, OrangePi, C.H.I.P. and i2cget/i2cset working environment.
* ADS1115
* typeK tyermocouple
* LM61CIZ

# hardware connection
                      ADS1115                      RaspberryPi
                  +------------+                    +-------+
                  |        ALART--Open              |       |
                  |            |                    |       |
    Thermo(Cr)----ANI0       SCL---------*----------SCL     |
                  |            |         |          |       |
    Thermo(Al)--*-ANI1       SDA---------+---*------SDA     |
                | |            |         |   |      |       |
       LM61CIZ--+-ANI2       VDD-----*---+---+------3.3V    |
        | |     | |            |     |   |   |      |       |
        | | NC--+-ANI3      ADDR-*---+---+---+---*--GND     |
        | |     | |            | |   |   |   |   |  |       |
        | |     | |          GND-+   |   |   |   |  |       |
        | |     | |            |     |   |   |   |  |       |
        | |     | +------------+     |   |   |   |  +-------+
        | |     |                    |   |   |   |
        | +-----+--------------------+---+---+---*
        |       |                    |   |   |   |
        +-------+--------------------+---+---*   |
                |                    |   |   |   |
                *---[R 2k Ohm]-------*   |   |   |
                |                    |   |   |   |
                *---[R 2k Ohm]-------+---+---+---*
                |                    |   |   |   |
                +---[C 0.1 uF]-------+---+---+---*
                                     |   |   |   |
                                     |   |   |   |
         AQM0802                     |   |   |   |
        +--------+                   |   |   |   |
        |        |                   |   |   |   |
        |      VDD-*-----------------+   |   |   |
        |        | |                     |   |   |
        |    RESET-+                     |   |   |
        |        |                       |   |   |
        |      SCL-----------------------+   |   |
        |        |                           |   |
        |      SDA----+                      |   |
        |        |    |                      |   |
        |      GND----+-*--------------------+---+
        |        |    | |                    |
        +--------+    | |                    |
                      | |                    |
                      | |                    |
         2SA1015      | |                    |
        +------+      *-+--[R 100k Ohm]------*
        |      |      | |                    |
        |      B------+ |                    |
        |      |        |                    |
        |      C--------+                    |
        |      |                             |
        |      E-----------------------------+
        |      |
        +------+
        (PNP Tr)
    
    
    + corner/cross-over
    * connect
(AQM0802 is optional, charactor LCD.)
