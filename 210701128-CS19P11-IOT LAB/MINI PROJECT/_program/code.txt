#include <Servo.h>
const int irSensorPin = 13; 
const int ledPin = 12;    
const int LDRpin1 = A0;
const int LDRpin2 = A1;
Servo servo;
void setup() 
{
  pinMode(irSensorPin, INPUT);
  pinMode(ledPin, OUTPUT);  

  Serial.begin(9600); 
  servo.attach(11); 
}

void loop() 
{
  float LDR1 = 1023 - analogRead(LDRpin1);
  float LDR2 = 1023 - analogRead(LDRpin2);
  int irValue = digitalRead(irSensorPin);
  Serial.print(irValue);
  Serial.println("LDR1");
  //delay(1000);
  Serial.print(LDR1);
  //delay(1000);
  int diff = LDR1 - LDR2;
  int angle = map(diff, -1023, 1023, 0, 180);
  servo.write(angle);
  Serial.println("LDR2");
  Serial.print(LDR2);
  if (irValue == LOW)
   {
    digitalWrite(ledPin, HIGH);
    delay(500); 
    digitalWrite(ledPin, LOW); 
  }
}
