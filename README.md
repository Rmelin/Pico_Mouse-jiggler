# Automatiseret museryster (Mouse jiggler) med Raspberry Pi Pico

## Beskrivelse

Denne kode er skrevet til en Raspberry Pi Pico, hvor den emulerer en USB-mus ved hjælp af Adafruit HID-biblioteket. Koden får musen til at bevæge sig automatisk frem og tilbage på skærmen, samtidig med at en LED tændes og slukkes.

# Funktioner

- Bevæger musen 10 pixels til højre, venter 0,1 sekunder.

- Bevæger musen 10 pixels til venstre, venter 55 sekunder.

- LED'en på GPIO 25 tændes og slukkes for at indikere, hvornår musen bevæger sig.

## Krav

- Raspberry Pi Pico med CircuitPython installeret

- Adafruit CircuitPython HID-biblioteket

- USB-forbindelse til en computer

## Installation

1. Installer CircuitPython på din Raspberry Pi Pico:

- Download den nyeste UF2-fil fra CircuitPython.org

- Sæt din Pico i boot mode (hold BOOTSEL-knappen nede, mens du tilslutter den til din computer)

- Træk UF2-filen over på drevet RPI-RP2

2. Kopiér biblioteket til din Pico:

- Download Adafruit CircuitPython HID fra GitHub

- Kopiér adafruit_hid-mappen til lib-mappen på drevet CIRCUITPY

3. Overfør koden:

- Omdøb scriptet til code.py

- Gem filen direkte på CIRCUITPY-drevet

4. Tilslut Pico til en computer

- Når Pico er tilsluttet via USB, vil den fungere som en mus og bevæge sig automatisk

## Kodeforklaring
```circuitpy 
import time
import usb_hid
from adafruit_hid.mouse import Mouse
import board
import digitalio

# Initialiser musen
mouse = Mouse(usb_hid.devices)

# Konfigurer LED på GPIO 25
led = digitalio.DigitalInOut(board.GP25)
led.direction = digitalio.Direction.OUTPUT

# Sluk LED og vent 10 sekunder før start
led.value = False
time.sleep(10)

while True:
    led.value = True  # Tænd LED
    mouse.move(x=10)  # Flyt musen til højre
    led.value = False  # Sluk LED
    time.sleep(0.1)    # Kort pause

    led.value = True  # Tænd LED igen
    mouse.move(x=-10)  # Flyt musen til venstre
    led.value = False  # Sluk LED
    time.sleep(55)     # Vent 55 sekunder
```
## Fejlfinding

Modulet 'usb_hid' mangler?

Sørg for, at du kører koden på en Raspberry Pi Pico med CircuitPython, ikke på din computer.

## Musen bevæger sig ikke?

Kontroller, at adafruit_hid-biblioteket er placeret i lib-mappen på CIRCUITPY.

Prøv at genstarte Pico ved at tage den ud og tilslutte den igen.

### Advarsel

Denne kode kan gøre din computer vanskelig at bruge, fordi musen bevæger sig automatisk! Hvis du vil stoppe scriptet, skal du frakoble din Raspberry Pi Pico.