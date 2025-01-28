# Arduino MKR NB 1500

The Arduino MKR NB 1500 is a microcontroller board designed to integrate Narrowband IoT (NB-IoT) and LTE-M communication into your projects. Ideal for remote and low-power applications, such as environmental monitoring, solar-powered devices, and field deployments, it ensures reliable connectivity in areas without traditional internet access.

Powered by an Arm® Cortex®-M0 32-bit SAMD21 microcontroller, the board features a u-blox SARA-R410M-02B module for cellular communication and a Microchip® ECC508 crypto chip for secure data transmission. It supports multiple LTE bands (Cat M1/NB1) for global coverage, compatible with operators like Telstra, Vodafone, and Verizon.

The MKR NB 1500 includes a built-in Li-Po battery charger, allowing it to switch seamlessly between USB power, external 5V sources, or battery operation, making it suitable for energy-efficient deployments. It offers 8 digital I/O pins, 7 analog inputs, PWM support, and UART, SPI, and I²C interfaces for versatile connectivity.

Compatible with the Arduino IoT Cloud, the MKR NB 1500 simplifies secure remote monitoring and control. Developers can also use a variety of MKR family shields to expand functionality, such as adding GPS, Ethernet, or environmental sensing capabilities. A microSIM card is required for cellular connectivity.

## Set Up

1. Install the board and MKRNB libary in Arduino IDE.

2. Flash the SerialSARAPassthrough example onto the board.

3. Download the [M-Center software](https://www.u-blox.com/en/product/m-center), run, and then connect the board to the [M-Center software](https://content.u-blox.com/sites/default/files/2024-11/m-center_02.10.00.exe) with sketch's default board rate which is 9600 `CONNECT|COM6|9600|Data bits:8|Parity:none|Stop bits:1|Flow ctrl:hardware`

4. APN Configuration: Set the correct APN for Telstra. For LTE-M/NB-IoT, use:
```bash
AT+CGDCONT=1,"IP","telstra.iot"
```

The response should be `OK`.

It can take 2 minutes for the board to connect to the network.

Note, signal strength is crucial for establishing a connection. You can check the signal strength with the following AT command:

```bash
AT+CSQ
```

The response will be in the format `+CSQ: <rssi>,<ber>`. The `<rssi>` value should be between 10-31 for a good signal. Values below 10 indicate poor signal strength.
If it's not connected to/registered on the network, `AT+CSQ` will respond `+CSQ: 99,99` `OK`. If you've just changed the setting, wait at least 2 minutes.

## Configuration:

**Automatically select the network operator:** `AT+COPS=0`
Sets the module to automatically select the network operator. `OK` confirms the setting.

**Manually Attempt Network Registration** and try to register with Telstra's network: `AT+COPS=1,2,"50501"`

**Check the current network operator:** `AT+COPS?` and responds `+COPS: 0,0,"Telstra Telstra",7` `OK` with the 7 meaning CAT-M1 (LTE-M) and 8 meaning NB-IoT.

**Check signal strength:** `AT+CSQ` will respond `+CSQ: <rssi>,<ber>`. The `<rssi>` value should be between 10-31 for a good signal. Values below 10 indicate poor signal strength.

**Check and Set MNO Profile:** `AT+UMNOPROF=100`
Profiles:

`0`: Factory default

`100`: Telstra (Australia) 

After setting the profile, restart the module with: `AT+CFUN=15`

**Change Radio Access Technology (RAT):**

Use the [ChooseRadioAccessTechnology Arduino example](https://github.com/Luen/Arduino-MKR-NB-1500/tree/main/ChooseRadioAccessTechnology) which uses these commands:

NOTE: You may need to Set MNO Profile (see above) for this to be successful. Also note that the example doesn't show if it errored.

Disconnect from the network: `AT+COPS=2`

Set Radio Access Technology (RAT): `AT+URAT=8`

Options:
`7` for CAT-M1 only.
`8` for NB-IoT only.
`7,8` for CAT-M1 preferred, NB-IoT as failover.
`8,7` for NB-IoT preferred, CAT-M1 as failover.
Apply changes and restart the modem:  `AT+CFUN=15`

**Network registration status:**
`AT+CEREG?` responds `+CEREG: 0,1`

**SIM card status:** `AT+CPIN?` responds `+CPIN: READY` confirming the SIM card is unlocked and ready.

**Power saving mode:** `AT+UPSV?` responds `+UPSV: 0` means power saving mode is disabled.

**Set current time:** `AT+CCLK="25/01/28,12:01:53+40"`
The response should be `OK`.
To check the time, use `AT+CCLK?`.
The repsonse should be `+CCLK: "25/01/28,12:01:53+40"` `OK`.

**Check for Supported AT Commands:** `AT+CLAC`

**Disconnect from the network:** `AT+COPS=2`

**Reset the Module:** AT+CFUN=15

## Resources

- [Arduino-MKR-NB-1500-Starter-Guide.pdf](https://github.com/Luen/Arduino-MKR-NB-1500/Arduino-MKR-NB-1500-Starter-Guide.pdf)
- [u-blox-CEL_ATCommands_(UBX-13002752).pdf](https://github.com/Luen/Arduino-MKR-NB-1500/u-blox-CEL_ATCommands_(UBX-13002752).pdf)
- [Device Network Settings for Australia](https://support.digitalmatter.com/en_US/lte-mnb-iot/australia-suggested-4g-settings)
- [Telstra Arduino MKR NB 1500 Mosquitto](https://github.com/telstra/arduino-mkr-nb-1500-mosquitto)
- [Connect to secure MQTT broker](https://portal.u-blox.com/s/question/0D52p00009AblwoCAB/how-do-you-configure-sara-r4-to-connect-to-secure-mqtt-broker)
