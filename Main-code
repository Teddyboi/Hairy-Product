#include "motor.h"
#include <Servo.h>
#include <SPI.h>
#include <WiFly.h>

Servo myservo;

const long calibrationTime = 10000;

const long SetupPause = 5000;
const long AvoidTime = 30000;

const int pirPin = 2;

const int sensorMin = 0;
const int sensorMax = 600;
const int photosensor = 100;


int phaseCase = 0;
int pirCase = 0;

unsigned long currentmillis = 0;
unsigned long previousmillis = 0;

int SensorValue = 0;

int pos90act = 0;
int pos180act = 0;
int pos0act = 0;

int act = 0;

const int motorRENPin = 13;
const int motorRIN1Pin = 12;
const int motorRIN2Pin = 11;

const int motorLENPin = 8;
const int motorLIN1Pin = 10;
const int motorLIN2Pin = 9;

const int rightSpeed = 150;
const int leftSpeed = 255;
const int turnSpeed = 200;
const int stopSpeed = 0;

Motor rightMotor (motorRIN1Pin, motorRIN2Pin, motorRENPin);
Motor leftmotor (motorLIN1Pin, motorLIN2Pin, motorLENPin);

#include <NewPing.h>

#define RTRIGGER_PIN 6   // Arduino pin tied to trigger pin on the ultrasonic sensor.
#define RECHO_PIN     7  // Arduino pin tied to echo pin on the ultrasonic sensor.
#define LECHO_PIN  5
#define LTRIGGER_PIN 4
#define MAX_DISTANCE 30
const int threshold = 20;   // an arbitrary threshold level that's in the range of the analog input
NewPing Lsonar(LTRIGGER_PIN, LECHO_PIN, MAX_DISTANCE);
NewPing Rsonar(RTRIGGER_PIN, RECHO_PIN, MAX_DISTANCE);

void setup() 
{
  digitalWrite(A3,LOW);
  pinMode(A3,OUTPUT);
  Serial.begin(9600);
  myservo.attach(3);
  pinMode(pirPin, INPUT);
  digitalWrite(pirPin, LOW);
}
  

void loop() {
  currentmillis = millis();
  int LanalogValue = Lsonar.ping();
  int RanalogValue = Rsonar.ping();

  int sensorReading = analogRead(A0);


  switch (phaseCase) {
    case 0:

    Serial.println("phaseCase0");

    if(sensorReading > photosensor){
      phaseCase = 1;
     previousmillis = currentmillis;
    }
    break;
    
    case 1:

    Serial.println("phaseCase1");

    if(LanalogValue&&RanalogValue > threshold)
  {
    rightMotor.backward(rightSpeed);
    leftmotor.backward(leftSpeed);
  }
  else if(LanalogValue > threshold)
  {
    rightMotor.forward(rightSpeed);
    leftmotor.backward(leftSpeed);
  }
  else if(RanalogValue > threshold)
  {
    rightMotor.backward(rightSpeed);
    leftmotor.forward(leftSpeed);
  }
  else 
  {
    rightMotor.forward(rightSpeed);
    leftmotor.forward(leftSpeed);
  }
  
  if(currentmillis - previousmillis >= AvoidTime){
    rightMotor.forward(stopSpeed);
    leftmotor.forward(stopSpeed);
    phaseCase = 2; 
  }

  break;

  case 2:

  Serial.println("phaseCase2");
  
  switch (pirCase) {
        case 0:
        
        Serial.println("case0");
    myservo.write(90);
    previousmillis = currentmillis;
    pirCase = 1;
    break;
    
    case 1:

    Serial.println("case1");
    
    if (currentmillis - previousmillis >= SetupPause){
      pirCase = 2;
    }
    break;
    case 2:

    Serial.println("case2");
    
    SensorValue = digitalRead(pirPin);
    if (SensorValue == HIGH){
      phaseCase = 1;
      pirCase = 0;
      break;
    }
    delay(50);
    SensorValue = digitalRead(pirPin);
    if (SensorValue == HIGH){
      phaseCase = 1;
      pirCase = 0;
      break;
    }
    delay(50);
    SensorValue = digitalRead(pirPin);
    if (SensorValue == HIGH){
      phaseCase = 1;
      pirCase = 0;
      break;
    }
    else{
    myservo.write(180);
    previousmillis = currentmillis;
    pirCase = 3;
    break;
    }

    case 3:

    Serial.println("case3");
    
        if (currentmillis - previousmillis >= SetupPause){
      pirCase = 4;
    }
    break;

    case 4:

    Serial.println("case4");
    
    SensorValue = digitalRead(pirPin);
    if (SensorValue == HIGH){
      phaseCase = 1;
      pirCase = 0;
      break;
    }
    delay(50);
    SensorValue = digitalRead(pirPin);
    if (SensorValue == HIGH){
      phaseCase = 1;
      pirCase = 0;
      break;
    }
    delay(50);
    SensorValue = digitalRead(pirPin);
    if (SensorValue == HIGH){
      phaseCase = 1;
      pirCase = 0;
      break;
    }

    else{
    myservo.write(0);
    previousmillis = currentmillis;
    pirCase = 5;
    break;
    }

    case 5:

    Serial.println("case5");
    
     if (currentmillis - previousmillis >= SetupPause){
      pirCase = 6;
    }
    break;

    case 6:

    Serial.println("case6");
    
    SensorValue = digitalRead(pirPin);
    if (SensorValue == HIGH){
      phaseCase = 1;
      pirCase = 0;
      break;
    }
    delay(50);
    SensorValue = digitalRead(pirPin);
    if (SensorValue == HIGH){
      phaseCase = 1;
      pirCase = 0;
      break;
    }
    delay(50);
    SensorValue = digitalRead(pirPin);
    if (SensorValue == HIGH){
      phaseCase = 1;
      pirCase = 0;
      break;
    }
    
    previousmillis = currentmillis;
    phaseCase = 3;
  }
    break;
  

  case 3:

  Serial.println("PhaseCase3");
      digitalWrite(A3, HIGH);
      rightMotor.forward(stopSpeed);
      leftmotor.forward(stopSpeed);
      delay(10000);
      digitalWrite(A3,LOW);

      phaseCase = 0;
      
      break;
}

}
