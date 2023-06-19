# Project-sensor-parkir-dan-rem-otomatis
#include <Wire.h>
#include <Servo.h>
#define Buzzer 10
#define trigPin 8
#define echoPin 9
long duration;
int distance = 0;
int PIR =4;
int sensor = 0;
Servo myservo;

void setup()
{
pinMode(trigPin, OUTPUT);
pinMode(echoPin, INPUT);
pinMode(Buzzer, OUTPUT);
Serial.begin(9600);
pinMode (PIR,INPUT);
Serial.begin(9600);
myservo.attach(2);
}

void loop()
{
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);
duration = pulseIn(echoPin, HIGH);
distance= duration*0.034/2;

if (distance > 10)
{
Serial.println(distance);

digitalWrite(Buzzer,LOW);
}
else if (distance < 10 && distance >= 8)
{
Serial.println(distance);
digitalWrite(Buzzer,HIGH);
delay(500);
digitalWrite(Buzzer,LOW);
delay(500);
}
else if (distance < 8 && distance >= 6 )
{
Serial.println(distance);
digitalWrite(Buzzer,HIGH);
delay(100);
digitalWrite(Buzzer,LOW);
delay(100);
}
else if (distance < 6 && distance >= 4 )
{
Serial.println(distance);
digitalWrite(Buzzer,HIGH);
delay(50);
digitalWrite(Buzzer,LOW);
delay(50);
}
else if (distance < 4 )
{
Serial.println(distance);
digitalWrite(Buzzer,HIGH);
delay(50);
}
sensor = digitalRead(PIR);
if (sensor==HIGH) {
myservo.write(180);
Serial.println("Buka Rem");
delay(2000);
} else {
myservo.write(90); }
}
