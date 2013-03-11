Chillmon Board v0.1
Copyright 2013 Ryan Pierce, rdpierce@pobox.com
https://github.com/RyanPierce/ChillmonBoard

Component RASPBERRYPI_B / RASBERRYPI_SHIELD modified from microBuilder
library, available at
http://www.microbuilder.eu/Projects/EagleFootprintLibrary.aspx

OVERVIEW

This board is a Raspberry Pi shield designed to be used with the Chillmon
application, available on Github at https://github.com/eastein/chillmon for 
the purposes of providing temperature control for fermenting beer!

INPUTS

J1-J8 are analog temperature sensors. The center pin is the signal, and the
end pins are power (+3.3V) and Ground. Power is indicated with the + 
symbol.

Each sensor connects to a channel on an MCP3008 10-bit ADC. This is 
connected to the Raspberry Pi as per the Adafruit tutorial available
here: http://learn.adafruit.com/send-raspberry-pi-data-to-cosm
Note that 4 of the Pi's GPIO pins are used for bit-banging SPI; the Pi's
native SPI is not used.

JP1 is a 0.1" header to determine the Vref voltage for the ADC conversion.
Two choices are provided; jumpering the left two pins provides a precision
1.0V reference, while jumpering the right two pins connects the 3.3V power
supply from the Pi. The regulation of this power supply is unknown. Using
1.0V leads to a lower temperature range (maximum is 50C / 122F) but provides
for a higher temperature resolution.

JP9 is a port for a chain of Dallas Semiconductor OneWire temperature
sensors, especially the DS18B20. Adafruit provides a tutorial here:
http://learn.adafruit.com/adafruits-raspberry-pi-lesson-11-ds18b20-temperature-sensing
As above, the center pin is the signal, and the end pins are power and 
ground. Power is marked with a + symbol. Many DS18B20's can be connected in
parallel. Note that the Adafruit Occidentalis distribution for the Raspberry
Pi includes the OneWire kernel driver. At present, the Chillmon software
does not support this. The board includes the 4.7k pullup resistor, which
is required for OneWire.

OUTPUTS

J10, J11, and J12 are digital outputs connected to GPIO pins on the Pi,
specifically 17, 21, and 22 respectively. Each pin has a 10k pulldown
resistor, which is critical because the Pi initializes all pins in input
mode; voltage on them can float high enough to trigger solid state relays,
which will quickly burn out an air conditioner compressor. Currently, the
Chillmon software assumes an air conditioner is connected to J10, however
in the future we would like to add a heater, as we have found that the 
temperature at Pumping Station: One in the winter often drops below our 
target ale fermenting temperature. Note that these outputs are current
limited by the Pi; it can directly drive a solid state relay.
