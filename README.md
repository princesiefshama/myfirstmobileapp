This app is created by MIT app inventor 

For IOT Engineering project using microcontroller ESP32

2.3 Mobile App description

The MIT app inventor is used to create the application. It is a website and a mobile app that uses block coding style as you can create great applications in simple blocks using some basic concepts.

Our Mobile app Consists of 3 pages: 

Welcome page 
Main page 
Keypad page

2.3.1 Used Mobile app components

2.3.1.1- Shown components

Buttons (with picture icon)
It is a component which has a lot of commands like “clicked” and “long clicked” and other main commands.

Unclickable picture  
It is used only in showing the value of seven segments in this project.

Clickable picture (limited tasks) 
It has only a “clicked” command and it is a picture with activating clickable property. We used it to make the app look better. 

Label
It is used as title to pages used in second and third pages. 

2.3.1.2- Hidden components

Web1 (WIFI control to send and receive data)
It is used in communication between mobile apps and ESP32 as the using http language and starts with sending and receiving http header.
We agree to set the IP of ESP32 with value 192.168.4.1 to make the communication easier between both. 
As it worked but calling it in codes after a certain event and if there is a response, we use the command “Web.GotText” to use it.   

Clock
It used to make a periodic flag as we set it to 1000 millisecond (1 second) and we use a command (when clock. Timer) to make a certain command which is checking current value which ESP32 displays on seven segments. 
The main thing in Clock that we had to activate Timeralwaysfires properties which makes the clock always work from start again after it reaches time out and if you deactivate this property the clock will work for only one time then stop till we start it again manually.

Text to speech
We use this component mainly to check that the mobile app got the correct instruction which we use as we make it say the required task name. 

 Sound
We used it as time delay between instructions by making mobile vibrates for only 100 milliseconds and this prevented any overlapping in instructions for both mobile app or ESP32 and we used it as a physical signal to the user which is vibration of the mobile.

AccelormeterSensor
It used to check that the mobile is not moving a lot as it used to detect if the mobile is shaking so it called text to speech to say “stop shaking” and this helped to check that we closed the app correctly too.
We used it as one from advises on the MIT app inventor website that in using instructions which send data from mobile to another device it is recommended to make the mobile fixed to prevent any error in signal.


2.3.2 Mobile app Pages

Each page contains a group of them and each one has its own task and codes and trigger, so the next part explains each page and its components and codes. 

2.3.2.1 - Welcome page

It contains 2 buttons (Welcome picture - Start picture) and 3 hidden components (web1 - text to speech – AccelometerSensor). 
First button is a welcome picture. When you click on it, you will hear welcome.
Second button is the start picture when you click on it, move you to the second screen and call text to speech to say, “start project”.
When you shake the mobile you will hear the app say to you “stop shaking” as AccelometerSensor feels the vibration that triggered it.   
Here we don’t use web1 in sending or receiving data, but we use it to prepare for next pages.

The main idea of this page is to welcome the user and wait for him to start the app by clicking on the start picture. 

2.3.2.2- Main page

It contains shown components (10 unclickable pictures for numbers from 0 to 9 - 3 buttons - 2 clickable pictures) and 5 hidden components (web1 - text to speech - Clock - Sound – AccelormeterSensor).  

3 buttons

Increment button 

When you click on it send it to URL (http://192.168.4.1/inc) to ESP32 by using WIFI module, when ESP32 receives it, it checks which instruction this interrupt is related then perform increment to the current value  and display the results on seven segment.

Decrement button

Same start as increment but its URL is (http://192.168.4.1/dec) and in this case ESP32 decrement the current value and display the result on seven 
segments.

Reset Button 

Same start as increment but its URL is (http://192.168.4.1/rst) and in this case ESP32 reset the current value (make it zero) and display the result on seven segments.

Unclickable picture for numbers from 0 to 9
As we use only one seven segments so we can display numbers from 0 to 9 so we present the value of seven segments on the mobile app as there is periodic check everyone second to make them equal whatever changes happened to them.
The pictures are the same number shapes on seven segments to be more realistic and clearer and they are controlled by switching property Visibility as the number we want to show we make it visible and other numbers not.

Clickable picture “STOP”

The main idea of this picture is to stop the mobile app and stop clocks because the clock works periodically and if you don’t stop it, will work in the background mobile and may cause useless problems so that Stop picture stops the clock and returns to the Welcome page to allow you to close the app safely. 

 Clickable picture “KEYPAD”

When you click on this picture it opens the keypad page where you can control the value of the seven segments directly without operations.

 Clock

It works periodically and gives a flag every one second. When mobile app gets this flag active it works the code in command “Clock. Time out” which is sending to URL (http://192.168.4.1/inc) to ESP32 by using WIFI module so ESP32 will send the current value back to mobile app to display it. 

 Sound

It is used as a delay between instructions to prevent overlapping between instructions and allow mobile apps to manage all of them.

 AccelormeterSensor

It used to check if the mobile was moving a lot, it called text to speech and made it say, “stop shaking”.

2.3.2.3- Keypad Page

It contains shown components (10 Clickable pictures for numbers from 0 to 9 - buttons) and 5 hidden components (web1 - text to speech - Sound - AccelormeterSensor).  

10 Clickable pictures for numbers from 0 to 9

Each number has its own URL (http://192.168.4.1/) after “/” we put the first three letters of this number (zer,one,two,thr,fou,fiv,six,sev,eig,nin) so when we click on it, mobile app send it to ESP32 by using WIFI module, when ESP32 receive it, it check its value and replace the current value with it  and display the results on seven segment.

Back Button

This button used to go back to the main screen and to check the current state of the seven segments.

Sound 
Same as before it used in making delay between instructions to prevent overlapping.
AccelormeterSensor
To check if the device is stable or not. 

2.3.3 The main idea of the codes in mobile app 

that mobile app waits till it gets interrupts of trigger by press button or picture to call the codes lines to execute them and the main codes instructions ideas are:
Going between screens (start and main and keypad) by using instruction (open another screen).
Calling Text to speech to say the instruction name for check that app take it correct
Sending data from mobile app to ESP32 by using WIFI module by using instructions (set web1 URL to, call web1)
Using a clock to check the current value of ESP32 every one second by setting the time interval to 1000 millisecond and instruction (when Clock. timer) and first check that property timeralwaysfire is activated 
Getting data from ESP32 by using code (when web1.gottext)
Using Accelerometer Sensor to check the stability of the device and there is no external movement by using instruction (when AccelormeterSensor. Shaking)
Using sound to make mobile vibrates for 100 milliseconds to prevent overlapping between instructions by instruction (call sound1.vibratie)
