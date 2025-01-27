# Arduino MKR NB 1500

The Arduino MKR NB 1500 is a microcontroller board designed to integrate Narrowband IoT (NB-IoT) and LTE-M communication into your projects. Ideal for remote and low-power applications, such as environmental monitoring, solar-powered devices, and field deployments, it ensures reliable connectivity in areas without traditional internet access.

Powered by an Arm® Cortex®-M0 32-bit SAMD21 microcontroller, the board features a u-blox SARA-R410M-02B module for cellular communication and a Microchip® ECC508 crypto chip for secure data transmission. It supports multiple LTE bands (Cat M1/NB1) for global coverage, compatible with operators like Telstra, Vodafone, and Verizon.

The MKR NB 1500 includes a built-in Li-Po battery charger, allowing it to switch seamlessly between USB power, external 5V sources, or battery operation, making it suitable for energy-efficient deployments. It offers 8 digital I/O pins, 7 analog inputs, PWM support, and UART, SPI, and I²C interfaces for versatile connectivity.

Compatible with the Arduino IoT Cloud, the MKR NB 1500 simplifies secure remote monitoring and control. Developers can also use a variety of MKR family shields to expand functionality, such as adding GPS, Ethernet, or environmental sensing capabilities. A microSIM card is required for cellular connectivity.

## Set up

Download the [M-Center software](https://www.u-blox.com/en/product/m-center) and loaded the SerialSARAPassthrough sketch from the Arduino examples onto the board.
Then connect the board to the [M-Center software](https://content.u-blox.com/sites/default/files/2024-11/m-center_02.10.00.exe) with sketch's default board rate is 9600 `CONNECT|COM6|9600|Data bits:8|Parity:none|Stop bits:1|Flow ctrl:hardware`

APN Configuration:
Set the correct APN for Telstra. For LTE-M/NB-IoT, use:

```bash
AT+CGDCONT=1,"IP","telstra.iot"
```

## Resources

Arduino-MKR-NB-1500-Starter-Guide.pdf
u-blox-CEL_ATCommands_(UBX-13002752).pdf
https://support.digitalmatter.com/en_US/lte-mnb-iot/australia-suggested-4g-settings
https://github.com/telstra/arduino-mkr-nb-1500-mosquitto