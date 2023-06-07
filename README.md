# Obstacle-Avoidance-Robot
Obstacle Avoiding Robot is an intelligent device that can automatically sense the obstacle in front of it and avoid them by turning itself in another direction. This design allows the robot to navigate in an unknown environment by avoiding collisions, which is a primary requirement for any autonomous mobile robot. 

//left motor pins
#define left_motor_a PB3
#define left_motor_b PB4
#define left_motor_pwm PA2
//right motor pins
#define right_motor_a PB5
#define right_motor_b PB6
#define right_motor_pwm PA3
//int s1 = PA5;   // sensor 1
//int s2 = PA6;  // sensor 2

#define trigger PB8
#define echo PB9

void setup() {
  // put your setup code here, to run once:

  pinMode(left_motor_a, OUTPUT);
  pinMode(left_motor_b, OUTPUT);
  pinMode(left_motor_pwm, OUTPUT);
  pinMode(right_motor_a, OUTPUT);
  pinMode(right_motor_b, OUTPUT);
  pinMode(right_motor_pwm, OUTPUT);

  pinMode (trigger, OUTPUT);
  pinMode (echo, INPUT);
  Serial.begin (9600);

}

void forward() {
  delay(10);
  digitalWrite(left_motor_a, HIGH);
  digitalWrite(left_motor_b, LOW);
  analogWrite(left_motor_pwm, 100); //0-255

  digitalWrite(right_motor_a, HIGH);
  digitalWrite(right_motor_b, LOW);
  analogWrite(right_motor_pwm, 100);
}
void left() {
  delay(10);
  digitalWrite(left_motor_a, LOW);
  digitalWrite(left_motor_b, HIGH);
  analogWrite(left_motor_pwm, 80);

  digitalWrite(right_motor_a, HIGH);
  digitalWrite(right_motor_b, LOW);
  analogWrite(right_motor_pwm, 0);
}


void right() {

  digitalWrite(left_motor_a, HIGH);
  digitalWrite(left_motor_b, LOW);
  analogWrite(left_motor_pwm, 0);

  digitalWrite(right_motor_a, LOW);
  digitalWrite(right_motor_b, HIGH);
  analogWrite(right_motor_pwm, 80);
}


void loop() {
  // put your main code here, to run repeatedly:
  long distance;
  long duration;

  digitalWrite (trigger, HIGH);
  delayMicroseconds (100);
  digitalWrite (trigger, LOW);
  delayMicroseconds (100);
  duration = pulseIn(echo, HIGH);
  distance = duration / 58.2;
  Serial.println(distance);

  if (distance > 50)
  {
    delay(100);
    forward();
    delay (100);
  }

  else if (distance < 50)

  {

    left();

  }

}
