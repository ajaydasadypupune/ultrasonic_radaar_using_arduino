# ultrasonic_radaar_using_arduino
//c programing language
#include <Servo.h>

const int trigPin = 9;
const int echoPin = 10;
Servo servoMotor;

void setup() {
  Serial.begin(9600);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  servoMotor.attach(6);  // Attach servo motor to pin 6
}

void loop() {
  for (int angle = 0; angle <= 180; angle += 5) {
    sweep(angle);
    delay(50);
  }
}

void sweep(int angle) {
  servoMotor.write(angle);
  delay(100);
  long duration, distance;

  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = (duration * 0.0343) / 2;

  printDistance(angle, distance);
}

void printDistance(int angle, long distance) {
  Serial.print("Angle: ");
  Serial.print(angle);
  Serial.print(" degrees, Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
}
