# Project description:

This is a children education tool that aims to let children have a brief understanding of pregnancy and knowing the process that their mother experienced. Symbol of wave represent fetal movement, other symbol likes eyes and ears would also grow bigger representing a significant development during particular month. Use M5 stack and receive analog input value from the heart pressed by putting a pressure sensor inside. People say that baby is sharing the same heart beat with their mother durning pregnancy, and heart also symbolize life. That's why I sewed a heart input to lead the change of different stages. 

# Hardware:

- Wire
- Fabric
- M5 Stack
- Pressure sensor
- Thread

# State Diagram
<img width="1152" alt="flow chart" src="https://github.com/user-attachments/assets/5b7f8a32-39f7-485d-a8bd-badd6d943172">

# Firmware

Thonny
```Python

adc = ADC(Pin(1), atten=ADC.ATTN_11DB)
adc_val = None

M5.begin()

while True:
  M5.update()
  
  # read analog value from ADC:
  adc_val = adc.read()
  
  print(adc_val)
  
  # remap the range of values from 0 - 4095 to 0 - 255:
  adc_val = int(m5utils.remap(adc_val, 0, 4095, 0, 255))
  
  time.sleep_ms(100)
```

Visual studio code
```Python

imu_data = [0, 0, 0]
data_string = None

image_list = [start, month11, month21, month31, month41, month51, month61, month71, month81, month91, ending]
image_list2 = [start, month12, month22, month32, month42, month52, month62, month72, month82, month92, ending]

image_counter = 0
sound1_played = False
```

```Python

def draw():
  global data_string
  global image_counter, sound1_played
  p5.background(0)
  p5.image(computer,-10,0)

  data = document.getElementById("data").innerText
  
  # assign content of "data" div on index.html page to variable:
  data_string = document.getElementById("data").innerText


  #p5.image(computer, 0, 0, 500, 400)
  if (p5.millis() % 1000 < 500):
    # show this image for 500 milliseconds:
    p5.image(image_list[image_counter], 15, -50, 500, 400)
  else:
    # show this image for next 500 milliseconds:
    p5.image(image_list2[image_counter], 15, -50, 500, 400)
  
  if (image_counter >1):
    p5.image(heart,50,40,70,70)

  if (image_counter == 4):
    p5.image(wave,400,220,80,80)
    p5.image(ear,60,220,50,50)
    p5.image(eye,400,50,50,30)
```

```Python
  if (image_counter == 10 and not sound1_played):
    sound1.play()
    sound1_played = True  # Update flag so sound1 only plays once

    # Only play the other sound if sound1 is not currently playing
  if (int(data_string) < 2000):
    if(sound.isPlaying() == False):
      sound.play()
      #sound.loop(True)
      if (image_counter < len(image_list)-1):
        image_counter += 1
      else:
        image_counter = 0
```

# Sketch
<img width="976" alt="Screenshot 2024-11-14 at 10 37 11 PM" src="https://github.com/user-attachments/assets/06c0cf9f-f5ef-425e-b4a7-a5ecfcc089d6">

# Outcome
![view](https://github.com/user-attachments/assets/180b3ee8-0b99-42f9-9ffd-02f7566a9951)
![heart](https://github.com/user-attachments/assets/ba13b227-ccc5-412c-97d2-f9b17dde2148)

Video
https://youtu.be/-GQHEz_UPbY
