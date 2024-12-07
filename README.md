# MG-EV-Inverter
Reverse engineering of the drive motor and inverter used in MG Electric Vehicles.

The drive unit here is from a 2022 MG ZS EV Right hand drive. 

First look : https://vimeo.com/929258328

IGBT Module : FS820R08A6P2B

Gate driver : MC33GD3100EK

One current sensor per phase. 5V supply, 2.5V at zero current anlog output.

Isolated gate power supplies provided from a common 30VDC primary supply , a pair of 5V at 132KHz and 42% duty signals to a mosfet driver. Transformers are Epcos A213721495C.

HV Voltage sensing is achived using the external ADC channel of the Low3 gate driver and transmitted via spi.

The three IGBT temp sensors are fed into the relevant high side drivers. Temp is sensed using the external ADC channel of the  three high side gate drivers and transmitted via spi.

The OEM logic board communicates with all 6 gate drive chips via SPI at a clock rate of 1.7MHz. Data is in 16 bit format with an 8 bit crc and sent/received as 24 bit packets.
Sadly , NXP want an NDA to allow access to the SPI data for this device. As this would then tie me down from sharing the data I will not be going this route. Instead, we'll use reverse engineering and open
information to discern the data formatting.

Freely available information has been found here :

https://community.nxp.com/t5/Other-NXP-Products/MC33GD3100-daisy-chain/td-p/1309335

and

https://community.nxp.com/t5/Power-Management/CRC-seed-value-for-MC33GD3100/m-p/1677961

and

https://community.nxp.com/t5/Motor-Control-and-Smart-Energy/GD3160-SPI-Example-code-Question/m-p/1780583

A series of SPI logic analyser captures are now here on the repo. Files are in Saleae Logic 2 format which my be freely downloaded here : https://www.saleae.com/pages/downloads

An Openinverter logic board replacement is currently being designed to allow this drive unit to be used unrestricted. Design files will be in Kicad format : https://www.kicad.org/

The external power and signal connector is a Molex 500762-1001 available from Mouser : https://www.mouser.ie/ProductDetail/538-500762-1001

The logic board to power board connector is a ERNI 063210-E available from Mouser : https://www.mouser.ie/ProductDetail/305-063210

The motor resolver and temp sensor connector is a TE 1897462-2 available from Mouser : https://www.mouser.ie/ProductDetail/571-1897462-2
Pins : https://www.mouser.ie/ProductDetail/571-7-1452656-3-CT

Gate driver signals are 5V level. One active low fault / INT line for high and low sides.

HV Connector may be Yonguui Metal Housing Connector-YG998C

V2 Logic board now undergoing testing.

Now working in closed loop FOC control with V2 logic board : https://vimeo.com/1032344714

Added 3D printable HV connector replacement. Also available on Printables : https://www.printables.com/model/1100211-mg-ev-drive-unit-high-voltage-connector



