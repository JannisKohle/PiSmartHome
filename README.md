# PiSmartHome

Backend and Frontend for a Smart Home System with a Raspberry Pi
which you can use the control lights, and do automation.

## About:

The backend is written in ```Node.js```, ```Express``` and ```MongoDB```. It can only
turn on / off lights, turn them on xyz %, and change the colors.
If you want to do automation, you can write bots that use the rest api to do more
complicated things.

There are client apps for iOS and desktop, written in Swift / Flutter and Electron.

## Automation / Bots:

If you want the lights to turn off automatically at some time, you can write a simple script
yourself that uses the rest api (see down below). You should then put the script onto the Raspberry
Pi, and run it. It wouldn't be smart to have the script on another machine, because then you would
have to have the Pi **and** your computer running at the same time.

If you don't want to run the script yourself, you can use the package.json inside the ```server/```.
Example:

I have a python script that should be automatically executed whenever the server on the RPi starts.
The script is outside the ```server/``` directory and it's called ```automationScript.py```. I can
add ``` && python3 ../automationScript.py``` to the end of the ```start``` script in
```server/package.json```, and now ```automationScript.py``` will be automatically executed whenever
I start the server using ```npm start```.

## The rest api:

### Add a new light:
- Endpoint: ```/lights```
- Method: ```POST```
- Body: ```{"name": "Bedroom Left", "PiGPIO": 34, "color": true}```
- Response: ```{"_id": "194b3f8271056de80a2cf14e", "name": "Bedroom Left", "PiGPIO": 34, "color": true, "turnedOn": false}```
- Possible Errors: Light with this name already exists; wrong GPIO

### Remove a light:
- Endpoint: ```/lights```
- Method: ```DELETE```
- Body: ```{"_id": "194b3f8271056de80a2cf14e"}``` or ```{"name": "Bedroom Left"}``` or ```{"PiGPIO": 34}```
- Response: ```{"_id": "194b3f8271056de80a2cf14e", "name": "Bedroom Left", "PiGPIO": 34, "color": true, "turnedOn": false}```
- Possible Errors: Light didn't exist

### Get a list of lights:
- Endpoint: ```/lights```
- Method: ```GET```
- Body: empty
- Response: ```[{...}, {...}, {...}]```
- Possible Errors: Light doesn't exist

### Get info about one light:
- Endpoint: ```/lights/{lightId}```
- Method: ```GET```
- Body: empty
- Response: ```{"_id": "194b3f8271056de80a2cf14e", "name": "Bedroom Left", "PiGPIO": 34, "color": true, "turnedOn": true}```
- Possible Errors: Light doesn't exist

### Change a light:
- Endpoint: ```/lights/{lightId}```
- Method: ```PATCH```
- Body: ```{"turnedOn": true}``` or ```{"name": "Living Room"}``` or ...
- Response: ```{"_id": "194b3f8271056de80a2cf14e", "name": "Living Room", "PiGPIO": 34, "color": true, "turnedOn": true}```
- Possible Errors: Light doesn't exist; Attribute in Body doesn't exist / Body wrong
- Info: This can be used to turn lights on / off, or change other attributes like ```PiGPIO```
