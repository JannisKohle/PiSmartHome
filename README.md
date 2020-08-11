# PiSmartHome

Backend and Frontend for a Smart Home System with a Raspberry Pi
which you can use the control lights, and do automation.

## About:

The backend is written in ```Node.js```, ```Express``` and ```MongoDB```. It can only
turn on / off lights, turn them on xyz %, and change the colors.
If you want to do automation, you can write bots that use the rest api to do more
complicated things.

There are client apps for iOS and desktop, written in Swift / Flutter and Electron.

## The rest api:

### Add a new light:
- Endpoint: ```/lights```
- Method: ```POST```
- Body: ```{"name": "Bedroom Left", "PiGPIO": 34, "color": true}```
- Response: ```{"_id": "194b3f8271056de80a2cf14e", "name": "Bedroom Left", "PiGPIO": 34, "color": true}```
- Possible Errors: Light with this name already exists; wrong GPIO

### Remove a light:
- Endpoint: ```/lights```
- Method: ```DELETE```
- Body: ```{"_id": "194b3f8271056de80a2cf14e"}``` or ```{"name": "Bedroom Left"}``` or ```{"PiGPIO": 34}```
- Response: ```{"_id": "194b3f8271056de80a2cf14e", "name": "Bedroom Left", "PiGPIO": 34, "color": true}```
