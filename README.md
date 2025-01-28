# Arduino MKR NB 1500

The Arduino MKR NB 1500 is a microcontroller board designed to integrate Narrowband IoT (NB-IoT) and LTE-M communication into your projects. Ideal for remote and low-power applications, such as environmental monitoring, solar-powered devices, and field deployments, it ensures reliable connectivity in areas without traditional internet access.

Powered by an Arm® Cortex®-M0 32-bit SAMD21 microcontroller, the board features a u-blox SARA-R410M-02B module for cellular communication and a Microchip® ECC508 crypto chip for secure data transmission. It supports multiple LTE bands (Cat M1/NB1) for global coverage, compatible with operators like Telstra, Vodafone, and Verizon.

The MKR NB 1500 includes a built-in Li-Po battery charger, allowing it to switch seamlessly between USB power, external 5V sources, or battery operation, making it suitable for energy-efficient deployments. It offers 8 digital I/O pins, 7 analog inputs, PWM support, and UART, SPI, and I²C interfaces for versatile connectivity.

Compatible with the Arduino IoT Cloud, the MKR NB 1500 simplifies secure remote monitoring and control. Developers can also use a variety of MKR family shields to expand functionality, such as adding GPS, Ethernet, or environmental sensing capabilities. A microSIM card is required for cellular connectivity.

## Set up

Install the board and MKRNB libary in Arduino IDE.

Flash the SerialSARAPassthrough example onto the board.

Download the [M-Center software](https://www.u-blox.com/en/product/m-center), run, and then connect the board to the [M-Center software](https://content.u-blox.com/sites/default/files/2024-11/m-center_02.10.00.exe) with sketch's default board rate which is 9600 `CONNECT|COM6|9600|Data bits:8|Parity:none|Stop bits:1|Flow ctrl:hardware`

APN Configuration:
Set the correct APN for Telstra. For LTE-M/NB-IoT, use:

```bash
AT+CGDCONT=1,"IP","telstra.iot"
```

The response should be `OK`.

Reset the board by disconecting from the software and reseting the board.

Note, signal strength is crucial for establishing a connection. You can check the signal strength with the following AT command:

```bash
AT+CSQ
```

The response will be in the format `+CSQ: <rssi>,<ber>`. The `<rssi>` value should be between 10-31 for a good signal. Values below 10 indicate poor signal strength.
If it's not registered on the network, `AT+CSQ` will respond `+CSQ: 99,99` `OK`.

Set current time:

```bash
AT+CCLK="25/01/28,12:01:53+40"
```

The response should be `OK`.
To check the time, use `AT+CCLK?`.
The repsonse should be `+CCLK: "25/01/28,12:01:53+40"` `OK`.

## Resources

- [Arduino-MKR-NB-1500-Starter-Guide.pdf](https://github.com/Luen/Arduino-MKR-NB-1500/Arduino-MKR-NB-1500-Starter-Guide.pdf)
- [u-blox-CEL_ATCommands_(UBX-13002752).pdf](https://github.com/Luen/Arduino-MKR-NB-1500/u-blox-CEL_ATCommands_(UBX-13002752).pdf)
- [Device Network Settings for Australia](https://support.digitalmatter.com/en_US/lte-mnb-iot/australia-suggested-4g-settings)
- [Telstra Arduino MKR NB 1500 Mosquitto](https://github.com/telstra/arduino-mkr-nb-1500-mosquitto)
