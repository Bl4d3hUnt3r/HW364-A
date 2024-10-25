HW-364A Pinout

The HW-364A / HW-364B is a cheap ESP8266 with 0.96 Inch OLED Display.


    SDA is D6 / GPIO14
    SCL is D5 / GPIO12
    Address is 0x3C

The HW-364A board uses the ESP8266 microcontroller. Here's a summary of the pinout:

    I2C Pins:
        GPIO12 (D5): I2C SCL (Clock)
        GPIO14 (D6): I2C SDA (Data)
    UART Pins:
        GPIO1 (TXD0): UART Transmit
        GPIO3 (RXD0): UART Receive
    General-purpose I/O Pins:
        GPIO0 (D3): Can be used as input/output, but has special boot function (flash mode)
        GPIO2 (D4): Can be used as input/output, but has special boot function (flash mode)
        GPIO4 (D2): Can be used as input/output
        GPIO5 (D1): Can be used as input/output
        GPIO13 (D7): Can be used as input/output
    SPI Pins: (not available for general GPIO use)
        GPIO6 to GPIO11

Notes on Pin Usage:

    Most GPIO pins can be used for general-purpose input/output.
    Pins can be configured as either input or output in your code.
    Some pins have special functions during boot mode, and their states determine the boot mode of the ESP8266.
    GPIO15 (D8) is active low, meaning it must be pulled high for normal boot.
    GPIO0, GPIO2, and GPIO15 have special functions during boot mode.

Internal Pull-up Resistors:

    All GPIO pins (D1-D7) have internal pull-up resistors that can be enabled.
    When a pin is not connected to GND, the internal pull-up resistor pulls the pin high (to 1).
    When a pin is connected to GND, the output changes to 0, confirming that the pull-up resistor is functioning correctly.

Output Functionality:

    All GPIO pins (D1-D7) can be used as outputs and can be configured to flash or output a specific value.


Example Code using U8g2

#include <U8g2lib.h>
#define OLED_RESET     U8X8_PIN_NONE // Reset pin
#define OLED_SDA 14                  // D6
#define OLED_SCL 12                  // D5

U8G2_SSD1306_128X64_NONAME_F_HW_I2C u8g2(U8G2_R0, OLED_RESET, OLED_SCL, OLED_SDA);

int c = 0;

void handle_oled(int c) {
  u8g2.clearBuffer();
  u8g2.setFont(u8g2_font_ncenB08_tr);
  u8g2.drawStr(0, 10, "Display is working!");
  u8g2.drawStr(0, 30, "Have fun with it");
  char buffer[20];
  snprintf(buffer, sizeof(buffer), "Uptime: %ds", c);
  u8g2.drawStr(0, 50, buffer);
  u8g2.sendBuffer();
}

void setup() {
  u8g2.begin();
}

void loop() {
  handle_oled(c);
  c++;
  delay(1000);
}

Full Pinout 

Pin Number	ESP8266 GPIO	Pin Name (HW-364A)	Functionality				            Notes
1		    GPIO16		    WAKE			    Wake from deep sleep		        	Can be used as a GPIO input/output
2		    GPIO1		    TXD0		    	UART Transmit	Default 		        TX pin for UART0
3		    GPIO3		    RXD0		    	UART Receive	Default 		        RX pin for UART0
4		    GPIO5		    D1			        General-purpose I/O			            Can be used as input/output
5		    GPIO4		    D2			        General-purpose I/O			            Can be used as input/output
6		    GPIO0		    D3			        General-purpose I/O			            Special boot function (flash mode)
7		    GPIO2		    D4			        General-purpose I/O			            Special boot function (flash mode)
8		    GPIO15		    D8			        General-purpose I/O			            Active low (must be pulled high for normal boot)
9		    GPIO6		    S2			        SPI Flash (not available for GPIO use)	Typically connected to internal SPI flash memory
10		    GPIO7		    S0			        SPI Flash (not available for GPIO use)	Typically connected to internal SPI flash memory
11		    GPIO8		    S1			        SPI Flash (not available for GPIO use)	Typically connected to internal SPI flash memory
12		    GPIO9		    S3			        SPI Flash (not available for GPIO use)	Typically connected to internal SPI flash memory
13		    GPIO10		    SC			        SPI Flash (not available for GPIO use)	Typically connected to internal SPI flash memory
14		    GPIO12		    D5			        I2C SCL (Clock)				            Can be used as input/output
15		    GPIO14		    D6			        I2C SDA (Data)				            Can be used as input/output
16		    GPIO13		    D7			        General-purpose I/O			            Can be used as input/output
