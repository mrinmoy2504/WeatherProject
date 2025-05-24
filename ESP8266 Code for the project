#include <ESP8266WiFi.h>

#define BLYNK_TEMPLATE_ID "TMPL61nFNGEDt"
#define BLYNK_TEMPLATE_NAME "nodemcu project"

#include <BlynkSimpleEsp8266.h>
#include <DHT.h>


// WiFi credentials
char ssid[] = "mrinmoy_dibyo";
char pass[] = "mrinmoy23";

// Blynk Auth Token
char auth[] = "WaTqkREZsvOacyHcnGe-IT4poNpsiQC9";

// DHT sensor pin
#define DHTPIN D7  // You can change this to the ESP32 pin you are using
#define DHTTYPE DHT11

DHT dht(DHTPIN, DHTTYPE);
BlynkTimer timer;

void sendSensorData() {
  float h = dht.readHumidity();
  float t = dht.readTemperature(); // or dht.readTemperature(true) for Fahrenheit

  if (isnan(h) || isnan(t)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }

  Blynk.virtualWrite(V0, t); // Send temperature to Virtual Pin V0
  Blynk.virtualWrite(V1, h); // Send humidity to Virtual Pin V1

  Serial.print("Temperature: ");
  Serial.print(t);
  Serial.print(" *C, Humidity: ");
  Serial.print(h);
  Serial.println(" %");
}

void setup() {
  Serial.begin(115200);
  Serial.println("DHT11 with Blynk");

  Serial.print("Connecting to WiFi: ");
  Serial.println(ssid);
  WiFi.begin(ssid, pass);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.println("WiFi connected!");

  Serial.print("Connecting to Blynk...");
  Blynk.begin(auth, ssid, pass);
  Serial.println(" Blynk connected!");

  dht.begin();

  // Send sensor data every 1 second (adjust as needed)
  timer.setInterval(1000L, sendSensorData);
}

void loop() {
  Blynk.run();
  timer.run();
}
