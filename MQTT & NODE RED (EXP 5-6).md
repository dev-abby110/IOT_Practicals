# MQTT

## Setup Instructions for IoT

### Setup Section

1. **Install Node-RED**
   Run the following command to install Node-RED globally with unsafe permissions:
   ```bash
   npm install -g --unsafe-perm node-red
   ```
   (This sets up Node-RED.)

2. **Download Mosquitto**
   Download Mosquitto from [https://mosquitto.org/download/](https://mosquitto.org/download/).
   (This sets up Mosquitto.)

   After downloading:

   - Navigate to `C:\Program Files\mosquitto` in your file manager.
   - Open Command Prompt in the Mosquitto folder:
     ```bash
     cd "C:\Program Files\mosquitto"
     ```

3. **Using Mosquitto**

   - **Subscribe to a Topic**
     Use the `mosquitto_sub` command to subscribe to a topic:
     ```bash
     mosquitto_sub -t "<name>"
     ```
     Example:
     ```bash
     mosquitto_sub -t "IOT/Sem6"
     ```

   - **Publish a Message**
     Use the `mosquitto_pub` command to publish a message:
     ```bash
     mosquitto_pub -t "<name>" -m "<message>"
     ```
     Example:
     ```bash
     mosquitto_pub -t "IOT/Sem6" -m "sir is absent today"
     ```

4. **Using Node-RED**
  ![Alt text](https://github.com/dev-abby110/IOT_Practicals/blob/main/img/Screenshot%202025-05-05%20120230.png)
  
  
 
   - **open This in browser** `http://127.0.0.1:1880/`
  
     ![image](https://github.com/user-attachments/assets/09c7f801-2f27-418b-bb2b-c100c0c94b3f)

   - **Set Up MQTT in Node-RED**
     - Drag and drop the Debug node and the MQTT In node onto the workspace.
     - Double-click the MQTT In node to open the side menu.
     - Follow these steps:
       - Click the **Add** button to create a new server.
       - Add the server name.
       - Set the server IP to `127.0.0.1` and port to `1883`.
       - Click **Add** (top right).
       - Add the server.
       - Enter the topic name `<name>` (matching the Mosquitto server topic).
       - Click **Done**.
     - Deploy the Node-RED server by clicking **Deploy** (top right).

![Screenshot 2025-04-27 000652](https://github.com/user-attachments/assets/afaebac1-297a-41c8-82d2-ade008db0a9e)

   - **Check if the Message is Received**
     Publish a message to check if it is received:
     ```bash
     mosquitto_pub -t "IOT/Sem6" -m "hello"
     ```

   - **Send a Message Using Node-RED**
     - Drag and drop the MQTT Out node onto the workspace.
     - Set it up as follows:
       ```yaml
       Name: [Whatever you want]
       Server: [Select your server]
       Topic Name: <name> (Mosquitto server topic)
       QoS: 1
       Retain: true
       ```
       - Click **Done**.
      
         ![Screenshot 2025-04-27 000741](https://github.com/user-attachments/assets/fd2ae6fa-a433-454c-ba8d-d5243a755934)
         ![Screenshot 2025-04-26 234648](https://github.com/user-attachments/assets/17e3d79a-d2f5-448f-933b-23a45f8f0a28)
         ![Screenshot 2025-04-27 000627](https://github.com/dev-abby110/IOT_Practicals/blob/main/img/Screenshot%202025-05-05%20121814.png)
     - Add an Inject node:
       - Configure `msg.payload` to be a string.
       - Add the message you want to send.
       - Click **Done**.
     - Deploy the Node-RED server by clicking **Deploy** (top right).
      
   - **Debug the Message**
     - Click the Debug icon.
     - Click the message button to see the message output.

![Screenshot 2025-04-27 002206](https://github.com/dev-abby110/IOT_Practicals/blob/main/img/Screenshot%202025-05-05%20120802.png)

   
