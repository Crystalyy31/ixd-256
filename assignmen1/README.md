# Assignment 1


## Project description:
This is a star night light that projects stars around the room after the light is turned off. In my childhood, my parents installed a star ceiling that shows up stars after the light is turned off. Slept with stars has become my habit, and it supports lots of fond dreams.

The project is made from cardboard with star shapes cut on all the pieces, and they were glued together to a hexagon shape. A RGB stripe is put inside the hexagon as the light source. The on and off toggle is the built-in button on the M5 Atom S3, while the other input is a moon-shaped cardboard that will change the color of the RGB stripe when in contact with the top of the hexagon.


## Hardware:
- Cardboard
- Wire
- Copper tape
- M5 Stack
- Breadboard
- Resistor
- Tape
  
## State diagram
<img width="1664" alt="Adv int" src="https://github.com/user-attachments/assets/71617561-6e50-4d93-9596-992054e99d44">

## Code
```Python
  import os, sys, io
import M5
from M5 import *
from hardware import *
import time

M5.begin()

input_pin = Pin(7, mode=Pin.IN, pull=Pin.PULL_UP)
input2_pin = Pin(41, mode=Pin.IN, pull=Pin.PULL_UP)

program_state = 'BLUE'
led_on = False
button_was_pressed = False
color_button_was_pressed = False

rgb2 = RGB(io=2, n=30, type="SK6812")

def get_rgb_color(r, g, b):
    return (r << 16) | (g << 8) | b

def turn_off_rgb():
    print("Turning off LEDs")
    rgb2.fill_color(0x000000)

def turn_on_rgb():
    global program_state
    print("Turning on LEDs with initial BLUE color")
    rgb2.fill_color(get_rgb_color(0, 0, 255))
    program_state = 'BLUE'

def change_rgb_color():
    global program_state
    if program_state == 'BLUE':
        program_state = 'PURPLE'
        purple = get_rgb_color(255, 0, 255)
        rgb2.fill_color(purple)
        for i in range(255):
            rgb2.fill_color(get_rgb_color(i, 255 - i, i))
            time.sleep_ms(5)
    elif program_state == 'PURPLE':
        program_state = 'BLUE'
        rgb2.fill_color(get_rgb_color(0, 0, 255))
        for i in range(255):
            rgb2.fill_color(get_rgb_color(255 - i, 0, i))
            time.sleep_ms(5)

def toggle_led_state():
    global led_on
    led_on = not led_on
    if led_on:
        turn_on_rgb()
    else:
        turn_off_rgb()

while True:
    M5.update()
    button_value = input2_pin.value()
    color_button_value = input_pin.value()
    time.sleep_ms(100)

    if button_value == 0 and not button_was_pressed:
        toggle_led_state()
        button_was_pressed = True
        time.sleep_ms(200)

    elif button_value == 1 and button_was_pressed:
        print("input2_pin released")
        button_was_pressed = False
    
    if led_on and color_button_value == 0 and not color_button_was_pressed:
        print("input_pin pressed - changing LED color")
        change_rgb_color()
        color_button_was_pressed = True
        time.sleep_ms(200)

    elif color_button_value == 1 and color_button_was_pressed:
        print("input_pin released")
        color_button_was_pressed = False
    
    time.sleep_ms(100)
```
