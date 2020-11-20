# remote_car
遥控车上的arduino部分代码
```
#include <SoftwareSerial.h>
#include <Servo.h>
Servo myservo1;
SoftwareSerial HC12(10, 11);
int gunPin = A2;
int rf1 = 2;
int rf2 = 3;
int lf1 = 4;
int lf2 = 5;
int rb1 = 6;
int rb2 = 7;
int lb1 = 8;
int lb2 = 9;
String data = "";
int motoInt = 80;
void setup() {
  // put your setup code here, to run once:
  Serial.begin(19200);
  HC12.begin(19200);
  pinMode(gunPin, OUTPUT);
  pinMode(rf1, OUTPUT);
  pinMode(rf2, OUTPUT);

  pinMode(lf1, OUTPUT);
  pinMode(lf2, OUTPUT);

  pinMode(rb1, OUTPUT);
  pinMode(rb2, OUTPUT);

  pinMode(lb1, OUTPUT);
  pinMode(lb2, OUTPUT);

  digitalWrite(rf1, 0);
  digitalWrite(rf2, 0);

  digitalWrite(lf1, 0);
  digitalWrite(lf2, 0);

  digitalWrite(rb1, 0);
  digitalWrite(rb2, 0);

  digitalWrite(lb1, 0);
  digitalWrite(lb2, 0);

  myservo1.attach(12);
  myservo1.write(motoInt);
}

void loop() {
  // put your main code here, to run repeatedly:
  
  while (HC12.available()) {
    data = char(HC12.read());
    Serial.println(data);
  }
  if (data == "W") {
    //    forward
    digitalWrite(rf1, 1);
    digitalWrite(rf2, 0);
    digitalWrite(lf1, 0);
    digitalWrite(lf2, 1);
    digitalWrite(rb1, 1);
    digitalWrite(rb2, 0);
    digitalWrite(lb1, 0);
    digitalWrite(lb2, 1);
  } else if (data == "X") {
    //    backward
    digitalWrite(rf1, 0);
    digitalWrite(rf2, 1);
    digitalWrite(lf1, 1);
    digitalWrite(lf2, 0);
    digitalWrite(rb1, 0);
    digitalWrite(rb2, 1);
    digitalWrite(lb1, 1);
    digitalWrite(lb2, 0);
  } else if (data == "A") {
    //    right
    digitalWrite(rf1, 1);
    digitalWrite(rf2, 0);
    digitalWrite(lf1, 1);
    digitalWrite(lf2, 0);
    digitalWrite(rb1, 0);
    digitalWrite(rb2, 1);
    digitalWrite(lb1, 0);
    digitalWrite(lb2, 1);
  } else if (data == "D") {
    //    left
    digitalWrite(rf1, 0);
    digitalWrite(rf2, 1);
    digitalWrite(lf1, 0);
    digitalWrite(lf2, 1);
    digitalWrite(rb1, 1);
    digitalWrite(rb2, 0);
    digitalWrite(lb1, 1);
    digitalWrite(lb2, 0);
  } else if (data == "Q") {
    //    RIGHT F
    digitalWrite(rf1, 0);
    digitalWrite(rf2, 0);
    digitalWrite(lf1, 0);
    digitalWrite(lf2, 1);
    digitalWrite(rb1, 1);
    digitalWrite(rb2, 0);
    digitalWrite(lb1, 0);
    digitalWrite(lb2, 0);

  } else if (data == "C") {
    //    LEFT B
    digitalWrite(rf1, 0);
    digitalWrite(rf2, 0);
    digitalWrite(lf1, 1);
    digitalWrite(lf2, 0);
    digitalWrite(rb1, 0);
    digitalWrite(rb2, 1);
    digitalWrite(lb1, 0);
    digitalWrite(lb2, 0);

  } else if (data == "E") {
    //    LEFT F
    digitalWrite(rf1, 1);
    digitalWrite(rf2, 0);
    digitalWrite(lf1, 0);
    digitalWrite(lf2, 0);
    digitalWrite(rb1, 0);
    digitalWrite(rb2, 0);
    digitalWrite(lb1, 0);
    digitalWrite(lb2, 1);

  } else if (data == "Z") {
    //    RIGHT B
    digitalWrite(rf1, 0);
    digitalWrite(rf2, 1);
    digitalWrite(lf1, 0);
    digitalWrite(lf2, 0);
    digitalWrite(rb1, 0);
    digitalWrite(rb2, 0);
    digitalWrite(lb1, 1);
    digitalWrite(lb2, 0);

  } else if (data == "J") {
    //    RIGHT R
    digitalWrite(rf1, 0);
    digitalWrite(rf2, 1);
    digitalWrite(lf1, 0);
    digitalWrite(lf2, 1);
    digitalWrite(rb1, 0);
    digitalWrite(rb2, 1);
    digitalWrite(lb1, 0);
    digitalWrite(lb2, 1);

  } else if (data == "L") {
    //    LEFT R
    digitalWrite(rf1, 1);
    digitalWrite(rf2, 0);
    digitalWrite(lf1, 1);
    digitalWrite(lf2, 0);
    digitalWrite(rb1, 1);
    digitalWrite(rb2, 0);
    digitalWrite(lb1, 1);
    digitalWrite(lb2, 0);

  } else if (data == "S") {
    //    stop
    digitalWrite(rf1, 0);
    digitalWrite(rf2, 0);
    digitalWrite(lf1, 0);
    digitalWrite(lf2, 0);
    digitalWrite(rb1, 0);
    digitalWrite(rb2, 0);
    digitalWrite(lb1, 0);
    digitalWrite(lb2, 0);
  }else if (data == "1"){
    if(motoInt <80){
      motoInt = motoInt + 5;
      myservo1.write(motoInt);
      Serial.println(motoInt);
      data = "";
    }
    
  }else if (data == "2"){
    if(motoInt > 25){
      motoInt = motoInt - 5;
      myservo1.write(motoInt);
      Serial.println(motoInt);
      data = "";
    }
    
  }else if(data == "F"){
    digitalWrite(gunPin, HIGH);
    delay(100);
    digitalWrite(gunPin, LOW);
    data = "";
  }
  while (Serial.available()) {
    HC12.write(Serial.read());
  }
}
```
