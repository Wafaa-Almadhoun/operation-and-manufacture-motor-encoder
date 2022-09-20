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
 2. DC Gear motor with two-channel Hall effect encoder .
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

#### 2. DC Gear motor with two-channel Hall effect encoder . 

1. Arduino ANO
2. DC Gear motor with two-channel Hall effect encoder [here](https://a.co/d/bWDbtmQ) 
3. bettrey  5 volt
3.breadboard

## Connections



#### 1. single channel optical encoder .


Connect the 5v output of the Arduino to the positive rail of the breadboard

Connect the ground to the negative rail of the breadboard

Connect the anod of the IR LED and photodiod the positive rail of the breadboard

Connect the kathod of the IR LED to the 220 ohm resistor then connect the another leg to the negative rail of the breadboard

Connect the kathod of the photodiod to the 3k ohm resistor then connect the another leg to the negative rail of the breadboard

Connect the kathod of the photodiod to the 3k ohm resistor then connect the another leg to the pin 2 in arduino 

#### 2. DC Gear motor with two-channel Hall effect encoder .

The Ground pin of the motor connects to GND of the Arduino.

Encoder A (sometimes labeled C1) of the motor connects to pin 2 of the Arduino.

Pin 2 of the Arduino will record every time there is a rising digital signal from Encoder A.

Encoder B (sometimes labeled C2) of the motor connects to pin 4 of the Arduino. The signal that is read off pin 4 on

the Arduino will determine if the motor is moving forward or in reverse. We’re not going to use this pin in this tutorial,

but we will use it in a future tutorial

The VCC pin of the motor connects to the 5V pin of the Arduino. This pin is responsible for providing power to the encoder.

For this project, you don’t need to connect the motor pins (+ and – terminals) to anything since you will be

turning the motor manually with your hand.


## Block diagram & simulation

 #### 1. single channel optical encoder .

![i channel](https://user-images.githubusercontent.com/64277741/191320617-4da9e310-3383-420a-8a35-84d1dee577b1.png)

Figure (1): single channel encoder circuit

we need to add interrupter disk between the IR LED and photodiod the disk should fit with the BLDC shaft 

![interrupter disk ](https://user-images.githubusercontent.com/64277741/191324445-2ab75529-4655-47d4-bbac-13bd7eefb659.png)

Figure (2): single channel encoder circuit with interrupter disk with 28 channels .

#### 2. DC Gear motor with two-channel Hall effect encoder .
  to see the circuit in Tinkercad click  [here](https://www.tinkercad.com/things/4VUspfQYDXj-powerful-densor/editel?tenant=circuits) 
  
![Powerful Densor](https://user-images.githubusercontent.com/64277741/191338523-2994b792-72df-47d7-8aef-ca62c6707b4b.png)

Figure (3): DC Gear motor with two-channel Hall effect encoder 


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
     

##  3. Suggestions to build a special encoder .

   at least two channels are cut out on the interrupter disk. Encoders with higher resolution requirements have multiple channels,
   sometimes up to a dozen. The photodetector outputs a pulse of maximum voltage when light hits it and there is no voltage when
   there is no light. Therefore, the output from the encoder will be digital signals. If the encoder has a single channel
   interrupter disc, there is only a pair of output cables. 

   A dual-channel interrupter disc has two sets of output cables. The number of output cables is twice the number of channels on the 
   interrupter disk. The digital output is used to calculate speed, angular shift, and direction of the motor.

so we need minimum 3 channel 


![1-119](https://user-images.githubusercontent.com/64277741/191328132-a5b70b52-70e4-4f6d-bdff-aa78c7a3076c.jpg)

 Figure (4): single channel encoder circuit with interrupter disk .
 
 the interrupter disk need to desiend to install in BLDC shaft 
 
 [here](https://www.cuidevices.com/product-spotlight/capacitive-incremental-encoders) is all the methods to get directional , position , speed and distance information for three channel encoder 
  
