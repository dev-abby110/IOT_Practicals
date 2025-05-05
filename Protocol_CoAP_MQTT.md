# Basics of Networking Protocols (CoAP, MQTT) and Cloud Platform (ThingSpeak) for IoT Applications

## Aim
To understand and implement IoT communication protocols (CoAP, MQTT) and integrate them with ThingSpeak cloud platform for real-time data monitoring and analysis.

## Material Required
1. Computer with internet access
2. Raspberry Pi or ESP8266 / ESP32 microcontroller
3. MQTT Brokers (e.g., Mosquitto)
4. ThingSpeak account
5. Python programming environment
6. CoAP client/server libraries
7. Network connectivity

## Theory

### 1. CoAP (Constrained Application Protocol)
- A lightweight protocol designed for constrained devices
- Works over UDP and follows a request-response model similar to HTTP
- Used in IoT applications for efficient communication between devices
- Key Features:
  * Built-in resource discovery
  * Support for multicast
  * Asynchronous message exchange
  * Very low overhead
  * URI support
  * RESTful architecture
  * Built-in content negotiation

### 2. MQTT (Message Queuing Telemetry Transport)
- A lightweight messaging protocol that works on a publish-subscribe model
- Operates over TCP and is ideal for low bandwidth IoT communication
- Key Features:
  * Quality of Service (QoS) levels
  * Persistent sessions
  * Last Will and Testament (LWT)
  * Retained messages
  * Topic-based message filtering
  * Bi-directional communications

### 3. MQTT Brokers
- MQTT Brokers (like Mosquitto) manage message exchanges between clients
- Core Functions:
  * Client authentication
  * Message reception and queuing
  * Message distribution to subscribers
  * Session management
  * Topic-based routing

### 4. ThingSpeak
- A cloud-based platform for IoT data collection and visualization
- Allows real-time data monitoring and analytics
- Supports REST API and MQTT for data communication
- Features:
  * Real-time data collection
  * MATLAB analytics
  * Data visualization
  * Device management
  * API support

## Protocol Comparison

| Feature | MQTT | CoAP |
|---------|------|-------|
| Transport Protocol | TCP | UDP |
| Communication Pattern | Publish/Subscribe | Request/Response |
| Message Overhead | Small | Very Small |
| QoS Options | Three levels (0,1,2) | Confirmable/Non-confirmable |
| Security | TLS/SSL | DTLS |
| Bandwidth Usage | Low | Very Low |
| Architecture | Centralized (Broker) | Decentralized |
| Message Format | Binary | Binary |
| Resource Discovery | No | Yes |
| Use Cases | Reliable messaging, Telemetry | Resource constrained devices, M2M |

## Architecture Diagrams

### MQTT Architecture
1. Setting up an MQTT Broker.
2. Implementing CoAP communication.
3. Sending data to ThingSpeak.

## Conclusion
Introduces network protocols CoAP and MQTT along with cloud integration using ThingSpeak.
