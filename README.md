 # EXPERIMENT--06-INTERFACING-DIGITAL-SENSOR-ON-RASPBERRY-PI-DEVELOPMENT-BOARD-
### NAME
### ROLL NO:
### DEPARTMENT 
### DATE

### AIM
interface the DHT11 digital temperature and humidity sensor with a Raspberry Pi development board and display real-time data.

### REQUIREMENTS:
Raspberry Pi board (any version with GPIO support)

DHT11 temperature and humidity sensor

10kΩ pull-up resistor (optional, for stable signal)

Breadboard and jumper wires

Python 3 installed on Raspberry Pi

Adafruit_DHT Python library

### THEORY:
The DHT11 is a digital sensor used to measure temperature and humidity. It has a single-wire digital interface, making it easy to connect with microcontrollers or development boards like the Raspberry Pi.

Temperature range: 0–50°C (±2°C accuracy)

Humidity range: 20–90% RH (±5% accuracy)

Output: Digital signal on a single data pin

The Raspberry Pi, with its GPIO header and Python support, can be programmed to read sensor data at periodic intervals.

### CIRCUIT DIAGRAM:
 ![image](https://github.com/user-attachments/assets/4da8be8e-498d-47cc-8d36-edeb1bc9a299)
 Figure-01 Circuit diagram for interfacing DHT-11

### Connections:

DHT11 Pin	Connected to Raspberry Pi
VCC	5V
DATA	GPIO423  (Pin 16)
GND	GND (Pin 6)

 
### PROCEDURE:
Wiring:
Connect the DHT11 sensor to the Raspberry Pi GPIO pins as shown above.

 Prepare the installation of CircuitPython libraries
To be able to easily communicate with some sensors, CircuitPython has been developed. So, before installing the specific DHT-library, we have to do some preparation work.

Open a terminal window and write following commands:

In our case, it is really important to use the latest version of Raspberry Pi OS ! Even if it takes some time, do not skip the next step !

sudo apt update
sudo apt full-upgrade
sudo apt install python3-pip
sudo pip3 install --upgrade setuptools
sudo reboot
Then install and run a script developed by Adafruit :

sudo pip3 install --upgrade adafruit-python-shell
wget https://raw.githubusercontent.com/adafruit/Raspberry-Pi-Installer-Scripts/master/raspi-blinka.py
sudo python3 raspi-blinka.py
The script will probably ask you to update your python version to Version 3. Choose : y
 
 
 Install the CircuitPython-DHT Library
Open a terminal window and write following commands:

pip3 install adafruit-circuitpython-dht
sudo apt-get install libgpiod2


open thonny python and writhe the python script as shown below 


### PYTHON SCRIPT 
 
`


import time
import board
import adafruit_dht
import psutil
//// first check if a libgpiod process is running. 
for proc in psutil.process_iter():
    if proc.name() == 'libgpiod_pulsein' or proc.name() == 'libgpiod_pulsei':
        proc.kill()
sensor = adafruit_dht.DHT11(board.D23)
while True:
    try:
        temp = sensor.temperature
        humidity = sensor.humidity
        print("Temperature: {}*C   Humidity: {}% ".format(temp, humidity))
    except RuntimeError as error:
        print(error.args[0])
        time.sleep(2.0)
        continue
    except Exception as error:
        sensor.exit()
        raise error
    time.sleep(2.0)`






## SCREENSHOT OF THE OUPT AND CIRCUIT 




    
## RESULT:
The DHT11 temperature and humidity sensor was successfully interfaced with the Raspberry Pi, and real-time data was retrieved and displayed.
