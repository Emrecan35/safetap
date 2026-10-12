# Gate controller firmware

Arduino Uno sketch for the turnstile: reads the card with the RC522, exchanges data with the edge processor over USB serial, and drives the servo gate, LCD, LEDs and buzzer.

Required Arduino libraries:

- `MFRC522` (RFID reader)
- `Servo` (built in)
- `LiquidCrystal_I2C` (LCD)

The sketch (`gate_controller.ino`) will be added in the prototype work package (WP-04).
