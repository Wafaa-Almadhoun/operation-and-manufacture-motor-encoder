# operation-and-manufacture-motor-encoder

## Table of contents
* [Introduction](#Introduction)
* [Technologies](#technologies)
* [Components required](#Components-required)
* [Connections](#Connections)
* [Block diagram & simulation ](#Block-diagram-&-simulation)



## Introduction
This project is to operating and manufacture motor encoder for BLCD scooter Hub Motor Kit, 48V 350W Wheel 8 in 
for calculate pulses per revolution وTo help determine the location of the robot and with additional sensors , click  [here](https://www.heidenhain.us/resources-and-news/types-of-encoders-and-applications/#:~:text=%20The%20Most%20Common%20Types%20of%20Encoders%20,counterpart%2C%20angle%20encoders%20measure%20rotation.%20These%2C...%20More%20)
to know more about different types of encoders and their applications .

 ,We will cover several topics : 👍 
 
 1. single channel optical encoder .
 2. DC motor with a built-in optical incremental rotary encoder .
 3. Suggestions to build a special encoder for our BLDC motor  .

## Technologies
Project is created with:
* Arduino IDE 1.18.15 [To Downloud](https://www.arduino.cc/en/software)
* AUTODESK TINKERCAD [Open](https://www.tinkercad.com/)
	
## Components required

#### 1. single channel optical encoder .
1. Arduino ANO
2. IR LED (infrared light-emitting diode)[here](https://a.co/d/3mZR21J)
3. IR photodiode (infrared light-receiver-diode) [here](https://a.co/d/3mZR21J)
4. jumper wirs
5. 2 resistors 220 ,  3K ohm 
6. bettrey  5 volt
7.breadboard

#### 2. DC motor with a built-in optical incremental rotary encoder .


## Connections

#### 1. single channel optical encoder .


Connect the 5v output of the Arduino to the positive rail of the breadboard

Connect the ground to the negative rail of the breadboard

Connect the anod of the IR LED and photodiod the positive rail of the breadboard

Connect the kathod of the IR LED to the 220 ohm resistor then connect the another leg to the negative rail of the breadboard

Connect the kathod of the photodiod to the 3k ohm resistor then connect the another leg to the negative rail of the breadboard

Connect the kathod of the photodiod to the 3k ohm resistor then connect the another leg to the pin 2 in arduino 



## Block diagram & simulation

 #### 1. single channel optical encoder .

![i channel](https://user-images.githubusercontent.com/64277741/191320617-4da9e310-3383-420a-8a35-84d1dee577b1.png)

Figure (1): single channel encoder circuit

we need to add interrupter disk between the IR LED and photodiod the disk should fit with the BLDC shaft 

![interrupter disk ](https://user-images.githubusercontent.com/64277741/191324445-2ab75529-4655-47d4-bbac-13bd7eefb659.png)

Figure (2): single channel encoder circuit with interrupter disk with 28 channels .


#### The Code 

// Encoder output to Arduino Interrupt pin. Tracks the pulse count.
#define ENC_IN_RIGHT_A 2
 
// Keep track of the number of right wheel pulses
volatile long right_wheel_pulse_count = 0;
 
void setup() {
 
  // Open the serial port at 9600 bps
  Serial.begin(9600); 
 
  // Set pin states of the encoder
  pinMode(ENC_IN_RIGHT_A , INPUT_PULLUP);
 
  // Every time the pin goes high, this is a pulse
  attachInterrupt(digitalPinToInterrupt(ENC_IN_RIGHT_A), right_wheel_pulse, RISING);
   
}
 
void loop() {
  
    Serial.print(" Pulses: ");
    Serial.println(right_wheel_pulse_count);  
}
 
// Increment the number of pulses by 1
void right_wheel_pulse() {
  right_wheel_pulse_count++;
}



     Compile the code by clicking the green checkmark in the upper-left of the IDE window.

     Connect the Arduino board to your personal computer using the USB cord.

     Load the code we just wrote to your Arduino board.

     Now, follow the following steps in the image below.
     
               
	       
	       1- open the serial monitor .
	       2- rotate the motor 360 degree .
	       3- Arduino will record the number of pulses .
	       
	       
	       When you open the Serial Monitor, the pulse count should be 0. 
	       
	       Using your hand, rotate the motor a complete 360-degree turn.

               Here is the output. We can see the number of pulses generated. 
     

### 2-servo motor rotate 90 degrees and back to 0 degree after 3 sec .[see here ](https://www.tinkercad.com/things/gbPPDKDpC4S-task-12-servo-motor-0-90/editel?sharecode=F5nGzvf_Q4hBc8hK6pDw1buUxTyYmv8P1hEopJZUgGc)
![1](https://user-images.githubusercontent.com/64277741/122786121-a5116f80-d2bc-11eb-9a95-e5d2b8a3b9ab.PNG)
Figure (3): Servo Motor at initial value (0 degree)

After 3 sec 
![1 2](https://user-images.githubusercontent.com/64277741/122786155-ae9ad780-d2bc-11eb-8f7c-c81f11a682b0.PNG)
Figure (4): Servo Motor at 90 degrees
After 6 sec back to 0 
![1](https://user-images.githubusercontent.com/64277741/122786121-a5116f80-d2bc-11eb-9a95-e5d2b8a3b9ab.PNG)
Figure (5): Servo Motor back from 90 to 0 degree

#### The code 
`#include <Servo.h> 
 
int servoPin = 3;
int servoPin2 = 5;
int servoPin3 = 7;
int servoPin4= 10;
int servoPin5= 13;


 Servo Servo1, Servo2, Servo3, Servo4, Servo5;
void setup() { 
   // We need to attach the servo to the used pin number 
   Servo1.attach(servoPin); 
Servo2.attach(servoPin2);
Servo3.attach(servoPin3); 
Servo4.attach(servoPin4);
Servo5.attach(servoPin5); 
 
}
void loop(){ 
delay(3000); 
  
Servo1.write(90); 
   
Servo2.write(90); 
    
Servo3.write(90); 
   

Servo4.write(90); 


Servo5.write(90); 
  
delay(3000);
  
Servo1.write(0);
Servo2.write(0);
Servo3.write(0);
Servo4.write(0);
Servo5.write(0);




}
`_


### 3- Control multiple servo motors using Potentiometer [see here](https://www.tinkercad.com/things/jBKW8pofJhZ-task-3-control-servo-motor-using-potentiometer/editel?sharecode=FqY5TjQ9On_IY1DgVje0gg_ci8Gl3PQnv6i9iKbzVOA)
At begin
![3](https://user-images.githubusercontent.com/64277741/122786908-75169c00-d2bd-11eb-9624-60cee51a1ea6.PNG)
Figure (6): Five Servo Motor with Five Potentiometers

After start simulation ![4](https://user-images.githubusercontent.com/64277741/122787141-b3ac5680-d2bd-11eb-97f9-08a8c668f9b1.PNG)
Figure (7): Changing the angles of Servo Motors according to change the angles of Potentiometers

#### The Code 
`#include <Servo.h>

Servo s;

Servo t;

Servo u;

Servo v;

Servo w;



int potpin = 0;
int potpin2 = 1;
int potpin3 = 2;
int potpin4 = 3;
int potpin5 = 4;

int val = 0;
int val2 = 0;
int val3 = 0;
int val4 = 0;
int val5 = 0;


void setup()
{

  s.attach(13);  // attaches the servo on pin 13 to the servo object
  t.attach(10);
  u.attach(7);
  v.attach(5);
  w.attach(3);
}

void loop()
{

val = analogRead(potpin);
val = map(val, 3, 1023, 0, 176);

s.write(val);

delay(25);

val2 = analogRead(potpin2);
val2 = map(val2, 0, 1023, 0, 180);

t.write(val2);

delay(25);

val3 = analogRead(potpin3);
val3 = map(val3, 0, 1023, 0, 180);

u.write(val3);

delay(25);

val4 = analogRead(potpin4);
val4 = map(val4, 0, 1023, 0, 180);

v.write(val4);

delay(25);

val5 = analogRead(potpin5);
val5 = map(val5, 0, 1023, 0, 180);

w.write(val5);

delay(25);

}
`_
##  3. Suggestions to build a special encoder .

   at least two channels are cut out on the interrupter disk. Encoders with higher resolution requirements have multiple channels,
   sometimes up to a dozen. The photodetector outputs a pulse of maximum voltage when light hits it and there is no voltage when
   there is no light. Therefore, the output from the encoder will be digital signals. If the encoder has a single channel
   interrupter disc, there is only a pair of output cables. 

   A dual-channel interrupter disc has two sets of output cables. The number of output cables is twice the number of channels on the 
   interrupter disk. The digital output is used to calculate speed, angular shift, and direction of the motor.

so we need minimum 3 channel 


![1-119](https://user-images.githubusercontent.com/64277741/191328132-a5b70b52-70e4-4f6d-bdff-aa78c7a3076c.jpg)

 Figure (3): single channel encoder circuit with interrupter disk .
 
 the interrupter disk need to desiend to install in BLDC shaft 
 
 [here](https://www.cuidevices.com/product-spotlight/capacitive-incremental-encoders) is all the methods to get directional , position , speed and distance information for three channel encoder 
  
