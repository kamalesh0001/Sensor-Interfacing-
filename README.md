# ULTRASONIC SENSOR INTERFACING
## AIM:
To measure the distance of the obstacle using ultrasonic sensor and display the value in serial monitor using Arduino UNO controller.
## Software required:
Arduino IDE </br>
Proteous
## PROCEDURE:
### Arduino IDE
Step1:Open the Arduino IDE </br>
Step2: Go to file and select new file option </br>
Step3:Type the program </br>
Step4:Go to file and select save option to save the program </br>
Step5:Go to sketch and select verify or compile options </br>
Step6:If no error Hex file will be generated in the temporary folder </br>
### Proteus
Step7:Open the Proteus software </br>
Step8:Go to file select new design and click ok button </br>
Step9:Select component mode and click pick devices from the library </br>
Step10:Type the component name in the keyword to select the components and click ok button </br>
Step11:Design the circuit as per the diagram </br>
Step12:Double click the Arduino controller and upload the hex file generated by Arduino IDE </br>
Step13:Click start button and check the output
## THEORY:
The HC-SR04 is an affordable and easy to use distance measuring sensor which has a range from 2cm to 400cm (about an inch to 13 feet).
The sensor is composed of two ultrasonic transducers. One is transmitter which outputs ultrasonic sound pulses and the other is receiver which listens for reflected waves. It’s basically a SONAR which is used in submarines for detecting underwater objects.
### HC-SR04 Ultrasonic Sensor Pinout
![image](https://user-images.githubusercontent.com/71547910/235331840-78ee92ea-1406-40f4-a6f7-a158e91126b3.png)

The sensor has 4 pins. VCC and GND go to 5V and GND pins on the Arduino, and the Trig and Echo go to any digital Arduino pin. Using the Trig pin we send the ultrasound wave from the transmitter, and with the Echo pin we listen for the reflected signal.
### How the HC-SR04 Ultrasonic Distance Sensor Works?
It emits an ultrasound at 40 000 Hz which travels through the air and if there is an object or obstacle on its path It will bounce back to the module. Considering the travel time and the speed of the sound you can calculate the distance.
![image](https://user-images.githubusercontent.com/71547910/235331902-3447f8ae-7024-4680-99c2-8e1225babfb7.png)

In order to generate the ultrasound we need to set the Trig pin on a High State for 10 µs. That will send out an 8 cycle ultrasonic burst which will travel at the speed of sound. The Echo pins goes high right away after that 8 cycle ultrasonic burst is sent, and it starts listening or waiting for that wave to be reflected from an object.If there is no object or reflected pulse, the Echo pin will time-out after 38ms and get back to low state.

![image](https://user-images.githubusercontent.com/71547910/235331916-543ba51e-84f4-4231-a50f-ff65cfed15b3.png)

If we receive a reflected pulse, the Echo pin will go down sooner than those 38ms. According to the amount of time the Echo pin was HIGH, we can determine the distance the sound wave traveled, thus the distance from the sensor to the object.
For that purpose we are using the following basic formula for calculating distance:

Distance = Speed x Time

We actually know both the speed and the time values. The time is the amount of time the Echo pin was HIGH, and the speed is the speed of sound which is 340m/s. There’s one additional step we need to do, and that’s divide the end result by 2. and that’s because we are measuring the duration the sound wave needs to travel to the object and bounce back.
![image](https://user-images.githubusercontent.com/71547910/235331957-1be2a7cc-1d61-4268-9bea-cd4337b448a0.png)

Let’s say the Echo pin was HIGH for 2ms. If we want the get the distance result in cm, we can convert the speed of sound value from 340m/s to 34cm/ms.

Distance = (Speed x Time) / 2 = (34cm/ms x 1.5ms) / 2 = 25.5cm.

So, if the Echo pin was HIGH for 2ms (which we measure using the pulseIn() function), the distance from the sensor to the object is 34cm.

## PROGRAM:
int trigPin = 9;	// TRIG pin int </br> 
echoPin = 8;	// ECHO pin </br>

float duration_us, distance_cm; </br>
</br>

void setup() { </br>
// begin serial port </br>
Serial.begin (9600); </br>
// configure the trigger pin to output </br>
mode pinMode(trigPin, OUTPUT); </br>
// configure the echo pin to input mode </br>
pinMode(echoPin, INPUT); </br>
}
</br>

void loop() { </br>
// generate 10-microsecond pulse to TRIG pin </br>
digitalWrite(trigPin, HIGH);  delayMicroseconds(10); </br>
digitalWrite(trigPin, LOW); </br>

// measure duration of pulse from ECHO pin </br>
duration_us = pulseIn(echoPin, HIGH); </br>

// calculate the distance </br>
distance_cm = 0.017 * duration_us; </br>

// print the value to Serial Monitor </br>
Serial.print("distance: "); </br…
## CIRCUIT DIAGRAM:
![image](https://github.com/kamalesh0001/Sensor-Interfacing-/assets/132887038/f23009e7-f834-4f47-b427-a5e83ca582c4)

## OUTPUT:
![image](https://github.com/kamalesh0001/Sensor-Interfacing-/assets/132887038/e40b804d-a33a-4682-9535-78a6fcd08e46)

## RESULT:
Thus the distance of the obstacle is measured using ultrasonic sensor and display the value in serial monitor using Arduino UNO controller.
