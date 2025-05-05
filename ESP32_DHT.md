# ESP32 DHT Temperature and Humidity Monitoring System

## Introduction
This project demonstrates how to create an IoT-based temperature and humidity monitoring system using an ESP32 microcontroller and DHT11/DHT22 sensor. The system collects environmental data and uploads it to ThingSpeak for remote monitoring and analysis.

## Objectives
- Set up an ESP32 with DHT11/DHT22 sensor
- Implement WiFi connectivity
- Collect temperature and humidity data
- Upload data to ThingSpeak cloud platform
- Monitor environmental conditions in real-time

## Hardware Requirements
1. ESP32 Development Board
2. DHT11 or DHT22 Temperature and Humidity Sensor
3. Breadboard
4. Jumper Wires
5. USB Cable for Programming
6. 10kΩ Resistor (Pull-up)

## Circuit Diagram
![ESP32 DHT Connection](https://github.com/user-attachments/assets/ae1ea700-4eaf-49d1-b4ad-9b96f21ba586)

### Connection Details
- Connect DHT sensor's VCC pin to ESP32's 3.3V
- Connect DHT sensor's GND pin to ESP32's GND
- Connect DHT sensor's DATA pin to ESP32's GPIO 4
- Add a 10kΩ pull-up resistor between VCC and DATA pins

## Software Requirements
1. Arduino IDE
2. Required Libraries:
   - WiFi.h
   - HTTPClient.h
   - DHT.h

## Setup Instructions
1. **Install Arduino IDE**
   - Download and install Arduino IDE
   - Add ESP32 board support through Board Manager

2. **Install Required Libraries**
   - Install DHT sensor library through Library Manager
   - Install ESP32 board support package

3. **ThingSpeak Setup**
   - Create a ThingSpeak account
   - Create a new channel
   - Note down your API Key

4. **Code Configuration**
   - Replace WiFi credentials
   - Update ThingSpeak API key
   - Select correct DHT type (DHT11/DHT22)

## Code Explanation

### Library Inclusion and Pin Configuration
```c
#include <WiFi.h>
#include <HTTPClient.h>
#include "DHT.h"

#define DHTPIN 4       // GPIO where the DHT sensor is connected
#define DHTTYPE DHT11  // Change to DHT22 if using DHT22
DHT dht(DHTPIN, DHTTYPE);

// Wi-Fi credentials
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";

// ThingSpeak settings
const char* server = "http://api.thingspeak.com/update";
String apiKey = "YOUR_THINGSPEAK_API_KEY";

void setup() {
    Serial.begin(115200);
    dht.begin();

    WiFi.begin(ssid, password);
    Serial.print("Connecting to WiFi");

    while (WiFi.status() != WL_CONNECTED) {
        delay(500);
        Serial.print(".");
    }
    Serial.println(" Connected!");
}

void loop() {
    if (WiFi.status() == WL_CONNECTED) {
        float temp = dht.readTemperature();
        float hum = dht.readHumidity();

        if (isnan(temp) || isnan(hum)) {
            Serial.println("Failed to read from DHT sensor!");
            return;
        }

        Serial.print("Temperature: ");
        Serial.print(temp);
        Serial.print(" °C, Humidity: ");
        Serial.print(hum);
        Serial.println(" %");

        HTTPClient http;
        String url = server + "?api_key=" + apiKey + "&field1=" + String(temp) + "&field2=" + String(hum);
        
        http.begin(url);
        int httpResponseCode = http.GET();
        
        if (httpResponseCode > 0) {
            Serial.println("Data sent to ThingSpeak successfully");
        } else {
            Serial.print("Error sending data: ");
            Serial.println(httpResponseCode);
        }
        
        http.end();
    } else {
        Serial.println("WiFi Disconnected");
    }

    delay(15000);  // Send data every 15 seconds
}


```



