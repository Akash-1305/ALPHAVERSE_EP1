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
cpp```
