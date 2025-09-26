# ALPHAVERSE_EP1

---

## Project 1 - PIR Motion Detector
```cpp
const int PIRpin = 8;
const int BUZpin = 13;
int PIRstate = 0;

void setup() {
 pinMode(BUZpin, OUTPUT);
 pinMode(PIRpin, INPUT);
 Serial.begin(9600);
 Serial.println("PIR Sensor Test Started...");
}

void loop() {
 PIRstate = digitalRead(PIRpin);
 Serial.print("PIR State: ");
 Serial.println(PIRstate);
 if (PIRstate == HIGH) {
  digitalWrite(BUZpin, HIGH);
 } else {
  digitalWrite(BUZpin, LOW);
 }
 delay(1000);
}
```

---

## Project 2 - LED Brightness Control
```cpp
const int analogInPin = A3;
const int OutPin = 9;
int sensorValue = 0;
int outputValue = 0;

void setup() {
 Serial.begin(9600);
}

void loop() {
 sensorValue = analogRead(analogInPin);
 outputValue = map(sensorValue, 0, 4095, 255, 0);
 analogWrite(OutPin, outputValue);
 Serial.print("sensor = ");
 Serial.print(sensorValue);
 Serial.print("\t output = ");
 Serial.println(outputValue);
 delay(20);
}
```

---

## Project 3 - LDR Controlled LED Lamp
```cpp
const int pinLDR = A3;
const int pinLedW = 13;
int thresholdvalue = 600;

void setup() {
  Serial.begin(9600);
  pinMode(pinLedW, OUTPUT);
}

void loop() {
  int sensorValue = analogRead(pinLDR);
  Serial.println(sensorValue);
  if(sensorValue > thresholdvalue) {
    digitalWrite(pinLedW, LOW);
  } else {
    digitalWrite(pinLedW, HIGH);
    delay(2000);
  }
}
```

---

## Project 4 - Temperature Controlled Buzzer/Fan
```cpp
const int pinNTC = A3;
const int pinBuz = 13;
int thresholdvalue = 200;

void setup() {
  Serial.begin(9600);
  pinMode(pinBuz, OUTPUT);
}

void loop() {
  int sensorValue = analogRead(pinNTC);
  if(sensorValue > thresholdvalue) {
    digitalWrite(pinBuz, HIGH);
  } else {
    digitalWrite(pinBuz, LOW);
  }
  Serial.println(sensorValue);
  delay(1000);
}
```

---

## Project 5 - LED Lamp with Switch
```cpp
const int buttonPin = 5;
const int ledPin = 13;
int buttonState = 0;

void setup() {
  pinMode(ledPin, OUTPUT);
  pinMode(buttonPin, INPUT);
}

void loop() {
  buttonState = digitalRead(buttonPin);
  if (buttonState == LOW) {
    digitalWrite(ledPin, HIGH);
  } else {
    digitalWrite(ledPin, LOW);
  }
}
```

---

## Project 6 - Musical Door Bell
```cpp
const int Speakerpin = 9;
const int pPin = 5;

#define NOTE_AS4 466
#define NOTE_D5 587
#define NOTE_E5 659
#define NOTE_F5 698
#define NOTE_G5 784
#define NOTE_A5 880
#define NOTE_AS5 932
#define NOTE_C6 1047
#define NOTE_D6 1175
#define NOTE_DS6 1245
#define NOTE_F6 1397

int melody[] = {
 698, 587, 466, 587, 698, 932, 1175, 1047, 932, 587, 659, 698,
};

float noteDurations[] = {
 8, 16, 8, 8, 8, 4, 8, 16, 8, 8, 8, 4
};

int musicLength = sizeof(melody) / sizeof(melody[0]);

void setup() {
 pinMode(pPin, INPUT);
}

void loop() {
 int pPinState = digitalRead(pPin);
 if (pPinState == LOW) {
   for (int thisNote = 0; thisNote < musicLength; thisNote++) {
     int noteDuration = 2000 / noteDurations[thisNote];
     tone(Speakerpin, melody[thisNote], noteDuration);
     int pauseBetweenNotes = noteDuration * 1.30;
     delay(pauseBetweenNotes);
     if (digitalRead(pPin) == HIGH) {
       break;
     }
   }
 } else {
   noTone(Speakerpin);
 }
}
```

---

## Project 7 - Mini DC Fan
```cpp
const int TactPin = 5;
const int FanPin = 9;
int TactState = 0;

void setup() {
 pinMode(FanPin, OUTPUT);
 pinMode(TactPin, INPUT);
}

void loop() {
 TactState = digitalRead(TactPin);
 if (TactState == HIGH) {
 digitalWrite(FanPin, HIGH);
 delay(3000);
 } else {
 digitalWrite(FanPin, LOW);
 }
}
```

---

## Project 8 - Water Level and Conductivity Indicator
```cpp
const int sensorPinR = A0;
const int sensorPinB = A1;
const int sensorPinG = A2;
const int ledPinR = 2;
const int ledPinB = 3;
const int ledPinG = 4;
const int BuzzerPin = 13;
const int threshold = 600;

int sensorValueR;
int sensorValueB;
int sensorValueG;

void setup() {
  pinMode(ledPinR, OUTPUT);
  pinMode(ledPinB, OUTPUT);
  pinMode(ledPinG, OUTPUT);
  pinMode(BuzzerPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  sensorValueR = analogRead(sensorPinR);
  sensorValueB = analogRead(sensorPinB);
  sensorValueG = analogRead(sensorPinG);

  if ((sensorValueR > threshold) && (sensorValueB < threshold) && (sensorValueG < threshold)) {
    digitalWrite(ledPinR, LOW);
  } else {
    digitalWrite(ledPinR, HIGH);
  }

  if ((sensorValueB > threshold) && (sensorValueG < threshold)) {
    digitalWrite(ledPinB, LOW);
  } else {
    digitalWrite(ledPinB, HIGH);
  }

  if ((sensorValueG >= threshold) && (sensorValueB > threshold) && (sensorValueR > threshold)) {
    digitalWrite(ledPinG, LOW);
    digitalWrite(BuzzerPin, HIGH);
  } else {
    digitalWrite(ledPinG, HIGH);
    digitalWrite(BuzzerPin, LOW);
  }

  Serial.print("R = ");
  Serial.print(sensorValueR);
  Serial.print(" | B = ");
  Serial.print(sensorValueB);
  Serial.print(" | G = ");
  Serial.println(sensorValueG);

  delay(200);
}
```
