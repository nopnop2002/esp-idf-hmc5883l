# esp-idf-hmc5883l
Display the orientation of HMC5883L with ESP32

First, find the offset value for each axis.   
As you can see, each axis is quite off-center.   
![hmc5883l-calib-1](https://user-images.githubusercontent.com/6020549/232182195-a9fb53d5-d6fc-4382-9a82-28cdb911a82d.jpg)

And display the orientation.   
![hmc5883l-heading-1](https://user-images.githubusercontent.com/6020549/232182731-8f6870b9-8ce6-4d14-a39c-34c1a8123ef7.jpg)

# Software requiment
ESP-IDF V4.4/V5.x.   
ESP-IDF V5.0 is required when using ESP32-C2.   
ESP-IDF V5.1 is required when using ESP32-C6.   


# Hardware requirements
HMC5883L 3-axis Electronic Compass   


# Wireing
|HMC5883L||ESP32|ESP32-S2/S3|ESP32-C2/C3/C6||
|:-:|:-:|:-:|:-:|:-:|:-:|
|VCC|--|3.3V|3.3V|3.3V||
|GND|--|GND|GND|GND||
|SCL|--|GPIO22|GPIO12|GPIO5|(*1)|
|SDA|--|GPIO21|GPIO11|GPIO4|(*1)|
|DRDY|--|N/C|N/C|N/C||

(*1)You can change it to any pin using menuconfig.   


# Caribration

```
git clone https://github.com/nopnop2002/esp-idf-hmc5883l
cd esp-idf-hmc5883l/calibrate
idf.py set-target {esp32/esp32s2/esp32s3/esp32c2/esp32c3/esp32c6}
idf.py menuconfig
idf.py flash
```


### Configuration   
To find the offset value, set the compass offset to 0.   
![config-top](https://user-images.githubusercontent.com/6020549/232182279-d0e97cef-1f45-4f86-9d71-b5c16fe77ebf.jpg)
![config-app](https://user-images.githubusercontent.com/6020549/232182280-c2ddc0bc-f2c2-462f-a6f2-d8a6e9664344.jpg)

### Execute calibration   
ESP32 acts as a web server.   
I used [this](https://github.com/Molorius/esp32-websocket) component.   
This component can communicate directly with the browser.   
Enter the following in the address bar of your web browser.   
```
http:://{IP of ESP32}/
or
http://esp32.local/
```

As you move the compass it plots the X, Y and Z values.   
X, Y, Z offset are displayed.   

![hmc5883l-calib-1](https://user-images.githubusercontent.com/6020549/232182195-a9fb53d5-d6fc-4382-9a82-28cdb911a82d.jpg)

### Execute calibration again   
If you set the offset you got from the calibration and run it again, the circle position will change.   

![hmc5883l-calib-2](https://user-images.githubusercontent.com/6020549/232182196-d71d4259-d06d-4207-a8a0-92eab2f3b20e.jpg)




# Display the orientation   



```
git clone https://github.com/nopnop2002/esp-idf-hmc5883l
cd esp-idf-hmc5883l/heading
idf.py set-target {esp32/esp32s2/esp32s3/esp32c2/esp32c3/esp32c6}
idf.py menuconfig
idf.py flash
```


### Configuration   
Sets the compass offset obtained by calibration.   
![config-top](https://user-images.githubusercontent.com/6020549/229249348-21ca8f80-e976-4ddb-8bca-435c475a3290.jpg)
![config-app](https://user-images.githubusercontent.com/6020549/229249346-0da21399-9640-4708-bdb6-beed7549d55a.jpg)


### View orientation   
ESP32 acts as a web server.   
I used [this](https://github.com/Molorius/esp32-websocket) component.   
This component can communicate directly with the browser.   
Enter the following in the address bar of your web browser.   
```
http:://{IP of ESP32}/
or
http://esp32.local/
```

Click the mouse to change the display.   
![hmc5883l-heading-1](https://user-images.githubusercontent.com/6020549/232182731-8f6870b9-8ce6-4d14-a39c-34c1a8123ef7.jpg)
![hmc5883l-heading-2](https://user-images.githubusercontent.com/6020549/232182732-710a315a-c8bc-406b-b39a-d050e84b6a26.jpg)

WEB pages are stored in the html folder.   
I used [this](https://canvas-gauges.com/) for gauge display.   
You can change the design and color according to your preference.   

