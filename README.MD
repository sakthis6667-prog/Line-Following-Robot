// Arduino Line Following Robot
// 2 IR Sensors + L298N Motor Driver

#define LEFT_SENSOR 2
#define RIGHT_SENSOR 3

#define ENA 5
#define ENB 6

#define IN1 8
#define IN2 9
#define IN3 10
#define IN4 11

const int MOTOR_SPEED = 150;

void setup() {

  pinMode(LEFT_SENSOR, INPUT);
  pinMode(RIGHT_SENSOR, INPUT);

  pinMode(ENA, OUTPUT);
  pinMode(ENB, OUTPUT);

  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);

  analogWrite(ENA, MOTOR_SPEED);
  analogWrite(ENB, MOTOR_SPEED);

  Serial.begin(9600);
}

void loop() {

  int leftSensor = digitalRead(LEFT_SENSOR);
  int rightSensor = digitalRead(RIGHT_SENSOR);

  Serial.print("Left: ");
  Serial.print(leftSensor);

  Serial.print(" | Right: ");
  Serial.println(rightSensor);

  // LOW = Line detected

  if (leftSensor == LOW && rightSensor == LOW) {

    // Move Forward
    moveForward();

  }

  else if (leftSensor == LOW && rightSensor == HIGH) {

    // Turn Left
    turnLeft();

  }

  else if (leftSensor == HIGH && rightSensor == LOW) {

    // Turn Right
    turnRight();

  }

  else {

    // Stop
    stopRobot();

  }
}

void moveForward() {

  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);

  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void turnLeft() {

  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);

  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void turnRight() {

  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);

  digitalWrite(IN3, LOW);
  digitalWrite(IN4, LOW);
}

void stopRobot() {

  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);

  digitalWrite(IN3, LOW);
  digitalWrite(IN4, LOW);
}