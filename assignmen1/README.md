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

## How it works
Press the built-in button on M5 Stack Atom3 to light up the starlight, the starlight will turn on blue. Then, put the moon-shaped board on top of the hexagon, and when they successfully contact, the light will gradually fade to purple. If you want the light to turn back to blue, contact the moon-shaped board again with the top of the hexagon. To turn off the light, press the built-in button again. 

## Fireware
```Python

#turning on and off rgb
def turn_off_rgb():
    print("Turning off LEDs")
    rgb2.fill_color(0x000000)

def turn_on_rgb():
    global program_state
    print("Turning on LEDs with initial BLUE color")
    rgb2.fill_color(get_rgb_color(0, 0, 255))
    program_state = 'BLUE'
```

```Python
# Toggle between BLUE and PURPLE color
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
```

```Python
# Toggle the LED state
def toggle_led_state():
    global led_on
    led_on = not led_on
    if led_on:
        turn_on_rgb()
    else:
        turn_off_rgb()
```

```Python
#loop
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
## Final outcome
![IMG_9710](https://github.com/user-attachments/assets/14c604c6-80fb-4387-a6eb-921caed0d54c)
![IMG_9712](https://github.com/user-attachments/assets/e0702912-d72c-4b73-ae0a-75412d51964a)

## Video
https://drive.google.com/drive/folders/1TwoJVAHyTVnVVu836VBqr0ybMw8AS0N7?usp=drive_link
