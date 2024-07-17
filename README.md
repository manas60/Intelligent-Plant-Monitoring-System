# Intelligent-Plant-Monitoring-System
code of Aurdino IDE:-

#define BLYNK_PRINT Serial
#define BLYNK_TEMPLATE_ID "TMPL33P2w8F6s"
#define BLYNK_DEVICE_NAME "irrigation system"
#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>
#include <DHT.h>
int soil = A0;
//int data = 0;
#define DHTPIN D2
#define DHTTYPE DHT11
DHT dht(DHTPIN, DHTTYPE);

char auth[] = "E_-3fTuTXLcNIVsN5AMyOCUQq03uEqYe";
char ssid[] = "VIVO V2025";
char pass[] = "Armaan45";
int RelayPin1 = D5;

}
String text = "";
void setup()
{

  Serial.begin(9600);
  pinMode(RelayPin1, OUTPUT);
  pinMode(pirPin, INPUT);
  digitalWrite(RelayPin1,   LOW);
  dht.begin();
  Blynk.begin(auth, ssid, pass);
}

void loop() {
  Blynk.run();
  text = " ";
  int soil = A0;
  int data = analogRead(soil);
  int maps = map(data, 0, 1023, 100, 0);
  float h = dht.readHumidity();
  float t = dht.readTemperature();
  if (maps > 55) {
    text = "Water full";
    digitalWrite(D5, LOW);

  }
  else {
    text = "Water needed";
    digitalWrite(D5, HIGH);


  }
  Blynk.virtualWrite(V0, t);
  Blynk.virtualWrite(V1, h);
  Blynk.virtualWrite(V2, maps);
  Blynk.virtualWrite(V4, text);
}
