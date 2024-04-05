# MG-EV-Inverter
Reverse engineering of the drive motor and inverter used in MG Electric Vehicles.

The drive unit here is from a 2022 MG ZS EV Right hand drive. 

First look : https://vimeo.com/929258328

IGBT Module : FS820R08A6P2B

Gate driver : MC33GD3100EK

One current sensor per phase. 5V supply, 2.5V at zero current anlog output.

Isolated gate power supplies provided from a common 30VDC primary supply , a pair of 5V at 132KHz and 42% duty signals to a mosfet driver. Transformers are Epcos A213721495C.

HV Voltage sensing is achived using an LM2903 comparator as a VCO fed through a digital isolator (2PI Semi 141E60Q). Signal is 1MHz, 5V at 52% duty with no HV applied.
Duty cycle drops with increasing HV Voltage.

The three IGBT temp sensors are fed into the relevant high side drivers. The analog / pwm output from the low voltage side of the igbt driver does not seem to be connected.
Presumed at this time that the igbt temp is sent via SPI.

The OEM logic board communicates with all 6 gate drive chips via SPI at a clock rate of 1.7MHz. Data is in 16 bit format with an 8 bit crc and sent/received as 24 bit packets.
Sadly , NXP want an NDA to allow access to the SPI data for this device. As this would then tie me down from sharing the data I will not be going this route. Instead, we'll use reverse engineering and open
information to discern the data formatting.

Freely available information has been found here :

https://community.nxp.com/t5/Other-NXP-Products/MC33GD3100-daisy-chain/td-p/1309335

and

https://community.nxp.com/t5/Power-Management/CRC-seed-value-for-MC33GD3100/m-p/1677961

A series of SPI logic analyser captures are now here on the repo. Files are in Saleae Logic 2 format which my be freely downloaded here : https://www.saleae.com/pages/downloads

An Openinverter logic board replacement is currently being designed to allow this drive unit to be used unrestricted.

The external power and signal connector is a Molex 500762-1001 available from Mouser : https://www.mouser.ie/ProductDetail/538-500762-1001

The logic board to power board connector is a ERNI 063210-E available from Mouser : https://www.mouser.ie/ProductDetail/305-063210




