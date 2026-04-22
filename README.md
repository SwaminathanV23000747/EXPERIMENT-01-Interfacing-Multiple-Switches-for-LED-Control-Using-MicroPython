# EXPERIMENT-01-Interfacing-Multiple-Switches-for-LED-Control-Using-MicroPython


 
## NAME: Swaminathan.V

## DEPARTMENT: CSE-IOT

## ROLL NO:212223110057

## DATE OF EXPERIMENT:21-04-2026

## AIM

To interface multiple switches with the Raspberry Pi Pico and control LEDs using MicroPython.

## APPARATUS REQUIRED

1. Raspberry Pi Pico - 1

2. Push Button Switches - 2

3. LEDs (Light Emitting Diodes) -3

4. Buzzer - 1

5. 330Ω Resistors -3

6. Breadboard

7. Jumper Wires

8. USB Cable

## THEORY

<img width="474" height="407" alt="image" src="https://github.com/user-attachments/assets/df0155b7-5b06-4276-aad3-0e114260605d" />

## FIGURE-01: RASPBERRY PI PICO PINOUT DIAGRAM

Raspberry Pi Pico is a microcontroller board based on the RP2040 chip. It supports MicroPython, making it suitable for IoT and embedded applications. The Raspberry Pi Pico is a compact microcontroller board featuring a 40-pin layout, including power, ground, GPIO, and communication interface pins. It operates with a dual-core ARM Cortex-M0+ processor and supports MicroPython and C/C++ programming.

The power pins include VBUS (5V from USB), VSYS (1.8V to 5.5V input), 3V3(OUT) (regulated 3.3V output), and multiple ground (GND) connections. The board offers 26 multi-purpose GPIO pins (GP0 to GP28), which can be used for digital input, output, PWM, and communication interfaces such as I2C, SPI, and UART. It also features three analog-to-digital converter (ADC) pins (GP26, GP27, GP28), used for reading analog sensor values, along with an ADC_VREF pin to set the reference voltage.

For communication, I2C (SDA, SCL), SPI (MOSI, MISO, SCK), and UART (TX, RX) interfaces are mapped across different GPIO pins, allowing seamless connectivity with sensors and peripherals. All GPIO pins support PWM (Pulse Width Modulation), making it useful for motor control, LED brightness adjustment, and sound applications. The BOOTSEL button enables USB mass storage mode for firmware flashing, while the DEBUG pins (SWD interface) provide debugging capabilities. With its low power consumption, flexible GPIO options, and rich interface support, the Raspberry Pi Pico is widely used for IoT, embedded systems, robotics, and automation projects.

## WORKING PRINCIPLE

## Experiment 1A:
1. The LEDs are connected as outputs in any three GPIO pins.

2. The Buzzer connected as output in any one LED connected GPIO pins.

3. A MicroPython script reads the switch states and controls the LEDs accordingly.

## Experiment 1B:

1. The switches are connected as inputs to GPIO pins of the Pico.

2. The LEDs are connected as outputs.

3. A MicroPython script reads the switch states and controls the LEDs accordingly.

### CIRCUIT DIAGRAM
## Experiment 1A

<img width="710" height="507" alt="image" src="https://github.com/user-attachments/assets/6bc88cc6-578c-4c45-a346-17d4804816ae" />

## FIGURE-02:  Circuit Diagram of Digital Output Interface 

1. Connect LED 1 to GPIO 0 via a 330Ω resistor, LED 2 to GPIO 2 via a 330Ω resistor and LED 3 to GPIO 4 via a 330Ω resistor.

2. Connect the Buzzer positive to either one pins GPIO 0 or GPIO 2 or GPIO 4.

3. Connect the other terminals of the LEDs and Buzzer to GND.

## Experiment 1B

<img width="940" height="576" alt="image" src="https://github.com/user-attachments/assets/6fc9a95f-28d4-4793-bf72-f60e34877c33" />

## FIGURE-03:  Circuit Diagram of Digital Input and Output Interface 


1. Connect switch 1 to GPIO 2 and switch 2 to GPIO 3.

2. Connect LED 1 to GPIO 13 via a 330Ω resistor.

3. Connect LED 2 to GPIO 16 via a 330Ω resistor.

4. Connect the other terminals of the switches to GND.

## PROGRAM (MicroPython)
'''
## Experiment 1A:
from machine import Pin, PWM
import time

red_led    = Pin(1, Pin.OUT)
yellow_led = Pin(7, Pin.OUT)
green_led  = Pin(14, Pin.OUT)
buzzer     = PWM(Pin(22))

while True:

    red_led.value(1)
    print("Red LED is ON")
    time.sleep(3)
    red_led.value(0)
    print("Red LED is OFF")
    time.sleep(1)

    yellow_led.value(1)
    print("Yellow LED is ON")
    time.sleep(2)
    yellow_led.value(0)
    print("Yellow LED is OFF")
    time.sleep(1)

    green_led.value(1)
    print("Green LED is ON")
    time.sleep(4)
    green_led.value(0)
    print("Green LED is OFF")
    time.sleep(1)

    buzzer.freq(1000)
    buzzer.duty_u16(32768)
    print("Buzzer is ON")
    time.sleep(2)
    buzzer.duty_u16(0)
    print("Buzzer is OFF")
    time.sleep(1)




## Experiment 1B:
from machine import Pin
import utime


switch1 = Pin(2, Pin.IN, Pin.PULL_DOWN)
switch2 = Pin(28, Pin.IN, Pin.PULL_DOWN)


led_left  = Pin(13, Pin.OUT)
led_right = Pin(18, Pin.OUT)

print("=== AND Gate Operation Started ===")
print("Flip BOTH switches to turn LEDs ON\n")

prev_state = None

while True:
    s1 = switch1.value()
    s2 = switch2.value()

    result = s1 and s2

    led_left.value(result)
    led_right.value(result)

    current_state = (s1, s2, result)
    if current_state != prev_state:
        print(f"Switch1: {'ON ' if s1 else 'OFF '}  |  Switch2: {'ON ' if s2 else 'OFF '}  |  AND Result: {'1 →  LEDs ON' if result else '0 →  LEDs OFF'}")
        prev_state = current_state

    utime.sleep(0.05)



## OUTPUT


## Experiment 1A:



## FIGURE-04: CIRCUIT CONNECTION
<img width="729" height="496" alt="Screenshot 2026-04-21 140249" src="https://github.com/user-attachments/assets/78f5ac96-f018-4787-a21d-29a7655f37fe" />



## FIGURE-05: CODE EXECUTION OUTPUT

<img width="245" height="220" alt="Screenshot 2026-04-21 140404" src="https://github.com/user-attachments/assets/10e6ea57-2928-40ec-99b7-710ab9c01a59" />


## FIGURE-06: LED AND BUZZER STATUS
<img width="736" height="481" alt="Screenshot 2026-04-21 140240" src="https://github.com/user-attachments/assets/12140e74-c64f-4ea8-a780-83ce8b2abf68" />
<img width="729" height="496" alt="Screenshot 2026-04-21 140249" src="https://github.com/user-attachments/assets/8c3823cd-2caa-43ae-bc1f-97da24e16747" />
<img width="729" height="496" alt="Screenshot 2026-04-21 140249" src="https://github.com/user-attachments/assets/5c867baf-2ba0-453a-b5e9-15d0e1ab64ed" />


## Experiment 1B:


## FIGURE-07: CIRCUIT CONNECTION
<img width="862" height="618" alt="image" src="https://github.com/user-attachments/assets/abe56a65-b1b8-43df-be9a-cb41d566f772" />



## FIGURE-08: CODE EXECUTION OUTPUT

<img width="622" height="100" alt="image" src="https://github.com/user-attachments/assets/ca23e0bf-683c-410a-bb69-47152104dd53" />


## FIGURE-09: LED STATUS BASED ON SWITCH INPUTS
<img width="749" height="468" alt="Screenshot 2026-04-21 144057" src="https://github.com/user-attachments/assets/948598b1-577b-4308-ab6c-9947eafa0e4e" />


## RESULTS

The multiple switches connected to the Raspberry Pi Pico successfully controlled the LEDs based on their states, confirming the proper interfacing of digital inputs and outputs.

