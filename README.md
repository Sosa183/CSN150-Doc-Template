# Cybersecurity : CSN150-Doc-Template

## Name of Project
ESP32 Introduction

## Purpose
In this project, I turned an ESP32-CAM into its own WiFi Access Point (AP) instead of connecting it to my home router. The goal was to follow the Random Nerd Tutorials "ESP32-CAM Access Point (AP)" guide, modify the CameraWebServer example in Arduino IDE, and document all the steps, problems, and solutions. When the project is working, I can connect my phone directly to the ESP32-CAM’s WiFi network and view the camera web page without an external router. 

## Equipment
* [ESP32Cam](https://www.amazon.com/Aideepen-ESP32-CAM-Bluetooth-ESP32-CAM-MB-Arduino/dp/B08P2578LV/ref=sr_1_3?crid=4FY0ECFW0ZX7&keywords=ESP32+Cam&qid=1678902050&sprefix=esp32+cam%2Caps%2C240&sr=8-3)

* [USB Micro Data Cable](https://www.amazon.com/AmazonBasics-Male-Micro-Cable-Black/dp/B0711PVX6Z/ref=sr_1_1_sspa?keywords=micro+usb+data+cable&qid=1678902214&sprefix=Micro+USB+data+%2Caps%2C89&sr=8-1-spons&psc=1&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUFaU0NaUVZHU1RFUlAmZW5jcnlwdGVkSWQ9QTA3NTA4MDVFVERCS01HVlgxM1YmZW5jcnlwdGVkQWRJZD1BMDE4NTE1NTIwWUdONkdWSzU1M1Amd2lkZ2V0TmFtZT1zcF9hdGYmYWN0aW9uPWNsaWNrUmVkaXJlY3QmZG9Ob3RMb2dDbGljaz10cnVl)

## Links to documentation

##### Main tutorial:
ESP32-CAM: Set Access Point (AP) for Web Server (Arduino IDE)
-https://randomnerdtutorials.com/esp32-cam-access-point-ap-web-server/

##### Other Links:


## Steps I followed
1. In your Arduino IDE, go to File > Examples > ESP32 > Camera > CameraWebServer.
   
3. At the top of the code, find the Wi-Fi lines and set them like this:
const char* ssid = "ESP32-CAM Access Point";
const char* password = "123456789";

4. Remove the “station” Wi-Fi code
In setup(), delete or comment out this part:
WiFi.begin(ssid, password);
while (WiFi.status() != WL_CONNECTED) {
  delay(500);
  Serial.print(".");
}
Serial.println("");
Serial.println("WiFi connected");

5. Add Access Point code instead
In setup(), add:

WiFi.softAP(ssid, password);

6. Upload the code to the ESP32-CAM

7. Connect with your phone

8. Open the camera web page

On that same device, open a browser.

Type this in the address bar:
http://192.168.4.1

9. The video streaming page should load.


## Problems

During this project, I ran into several issues. At first, the ESP32-CAM wasn’t showing up as a Wi-Fi network because I didn’t remove the original WiFi.begin() station code. Then I had trouble finding the correct IP address because WiFi.localIP() always returned 0.0.0.0 in access point mode. I also had problems loading the web page until I disabled auto-switching on my phone’s Wi-Fi so it would stay connected to the ESP32 network. When compiling, I got an error with the server.send() function and had to change it to server.send_P() to match the updated ESP32 library. I also dealt with camera startup issues due to low power, and uploading the code failed until I put the ESP32-CAM into flash mode correctly. After resolving all these issues, the access point functioned properly, and I was able to access the camera page at 192.168.4.1.

## Final Report
