# Wiring (Arduino Uno)

## RC522 RFID reader (SPI, 3.3 V only)

| RC522 pin | Arduino Uno |
|---|---|
| SDA (SS) | D10 |
| SCK | D13 |
| MOSI | D11 |
| MISO | D12 |
| IRQ | not connected |
| GND | GND |
| RST | D9 |
| 3.3V | 3.3V (**not 5V**) |

## Gate and feedback

| Component | Arduino Uno |
|---|---|
| SG90 servo signal (orange) | D6 |
| SG90 servo power (red) / ground (brown) | 5V / GND |
| Green LED (+ 220 Ω resistor) | D4 |
| Red LED (+ 220 Ω resistor) | D5 |
| Buzzer (+) | D7 |
| LCD I2C SDA | A4 |
| LCD I2C SCL | A5 |
| LCD I2C VCC / GND | 5V / GND |

## Notes

- The RC522 runs on 3.3 V; connecting it to 5 V can damage it.
- If the servo makes the board reset, power it from a separate 5 V supply and connect the grounds together.
- The usual I2C address of the LCD module is `0x27` (sometimes `0x3F`).

## Parts list

| Part | Qty |
|---|---|
| Arduino Uno R3 compatible + USB cable | 1 |
| RC522 RFID kit (reader, card, key fob) | 1 |
| Extra 13.56 MHz MIFARE Classic 1K cards | 5 |
| SG90 micro servo | 1 |
| 16x2 LCD with I2C module | 1 |
| Breadboard (830 points) | 1 |
| Jumper wires (male-male, male-female) | 1 set |
| 5 mm LEDs (green, red) | 2+ |
| 220 Ω resistors | 2+ |
| Active buzzer | 1 |
