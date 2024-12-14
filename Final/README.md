# The Ebbing blue life


## Project description:
This is a children's education art installation that aims to raise awareness for marine pollution. The project will start by watching an educational video that highlights the biodiversity and fun facts about the ocean. At the same time, a light will fade in and out of the bowl, representing the breathing of life. After seeing the prompt near the end of the video, children would interact with the bowl by putting trash into the bowl and seeing the change that it brought to marine life. 


## Hardware:
- Fish bowl
- Thread
- Fabric
- Wire
- Atom3 boards
- Atom3 extension
- Breadboard
- Resistor
- Pressure sensor
- 3D printed sphere
- 
  
## State diagram
<img width="2142" alt="flow" src="https://github.com/user-attachments/assets/e5fbfc45-6bd7-415d-8421-d7c26fb21759" />

## hardware connection
<img width="1088" alt="Chart" src="https://github.com/user-attachments/assets/379f7ab5-5709-4af7-9c14-4c07a45d0fed" />

## How it works
It will start with video 1 playing, along with the light fadding in and out to represent the breathing. After seeing the promopt, user would put fabricated trash 

## Fireware
Thonny
```Python

#LED fadding 
  if (adc_val < 4000):
      #for i in range(256, -1, -1):
      #    rgb_strip.fill_color(get_rgb_color(0, i, 255))
      if (max_brightness is not 50):
          max_brightness = 50
          sensor3_label.setText('led: ' + str(max_brightness))
          
  if (adc_val1 < 4000):
      #for i in range(256, -1, -1):
      #    rgb_strip.fill_color(get_rgb_color(0, 0, i))
      if (max_brightness is not 0):
          max_brightness = 0
          sensor3_label.setText('led: ' + str(max_brightness))
```
Visual studio code
```Python
# Receiving value from thonny
global data, program_state, program_state2
  data_string = document.getElementById("data").innerText

  p5.image(myVid, 0, 0, p5.width, p5.height)

  # split data_string by comma, making a list:
  data_list = data_string.split(',')

  # check how many items the list contains:
  if (len(data_list)== 2): # received 2 values
    # assign 1st item of data_list to sensor_val:
    sensor_val = int(data_list[0])
    # assign 2nd item of data_list to sensor_val1:
    sensor_val1 = int(data_list[1])
  elif (len(data_list) == 1): # received only 1 value
    # assign 1st item of data_list to sensor_val:
    sensor_val = int(data_list[0])
    # assign 0 to button_val
    #button_val = 0
```

```Python
# Toggle state to control the falling of trash and video changing.
 if int(sensor_val1) < 4000:
        if program_state2 != "on":
            # Start the 5 seconds delay for the second video
          timer1 = p5.millis()
          myVid.stop()  # Stop the first video
          myVid1_playing = True
          program_state2 = "on"

    # After 5 seconds, play myVid2 and stop myVid
  if program_state2 == "on":

        if p5.millis() > timer1 + 3000:
          myVid2.play()  # Start playing the second video after 5 seconds
          myVid2.loop()  # Ensure it loops
          p5.image(myVid2, 0, 0, p5.width, p5.height)  # Show myVid2
        else:
          #p5.image(myVid, 0, 0, p5.width, p5.height)  # Show myVid until 5 seconds have passed
        #if myVid.stop():
          trash6.update6()
          trash7.update7()
          trash8.update8()
          trash5.update5()

  if (int(sensor_val) < 4000):

    if (program_state != "on"):
      # update timer1 to current time
      timer1 = p5.millis()  

    program_state  = "on"
    #sound.play()
    #sound_played = True
    
  if(program_state  == "on"):
    myVid.volume(0.5)
    trash1.update4()
    trash2.update()  
    trash3.update2()
    trash4.update3()

  else:
    myVid.volume(1.0)
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
![IMG_0902](https://github.com/user-attachments/assets/30c3b3a7-27e6-4a20-b03a-3d6181ac1eeb)


## Demo video
[https://drive.google.com/drive/folders/1TwoJVAHyTVnVVu836VBqr0ybMw8AS0N7?usp=drive_link
](https://youtu.be/IjbDehdUDRc)
