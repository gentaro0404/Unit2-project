![weather.png](weather_asbt.png)

# Unit 2: A Distributed Weather Station for ISAK

## Criteria A: Planning

### Problem definition
Daiichiro is a parent who has a student at ISAK. He is very concerned about his son's recent health problems. He is a data scientist, so he is very logical and only believes in data. And he wants data on the indoor and outdoor temperature and humidity in his son's room for 48 hours. And that data needs to be more accurate. And since the budget he is giving me is small, I need to get the resources at a low price.


### Proposed Solution
Considering the client requirements an adequate solution includes a low cost sensing device for humidity and temperature and a custom data script that process and anaysis the samples acquired. For a low cost sensing device an adequate alternative is the DHT11 sensor[^1] which is offered online for less than 5 USD and provides adequare precision and range for the client requirements (Temperature Range: 0°C to 50°C, Humidity Range: 20% to 90%). Similar devices such as the DHT22, AHT20 or the AM2301B [^2] have higher specifications, however the DHT11 uses a simple serial communication (SPI) rather than more eleborated protocols such as the I2C used by the alternatives. For the range, precision and accuracy required in this applicaiton the DHT11 provides the best compromise. Connecting the DHT11 sensor to a computer requires a device that provides a Serial Port communication. A cheap and often used alternative for prototyping is the Arduino UNO microcontroller [^3]. "Arduino is an open-source electronics platform based on easy-to-use hardware and software"[^4]. In additon to the low cost of the Arduino (< 6USD), this devide is programable and expandable[^1]. Other alternatives include diffeerent versions of the original Arduino but their size and price make them a less adequate solution.

Considering the client's budget constraints and hardware requirements, the software tool proposed for this solution was Python, which is open source, mature, supported on multiple platforms including macOS, Windows, and can be used for programming Arduino microprocessors56. It can also be used for programming the Arduino microprocessor56. It also has many developer tools available, making it easy to obtain information about problems that are difficult to solve.6 Python is a High Level Programming Language (HLL) with a higher level of abstraction than C or C++.7 For example, a C/C++ developer can allocate and free memory, whereas in Python, memory management is automatic, which can speed up applications, but can also cause memory problems. Furthermore, the HLL language allows me and future developers to extend the solution and solve problems quickly.

**Design statement**
Design Statement, We are creating a poster for our client, daiichirom. To do this, we need certain statistical data. That data will include a system diagram, a 48-hour visual representation and model of humidity and temperature in ISAK's rooms and ISAK's remote indoor areas, and a forecast for the next 12 hours. Health implications for humidity and temperature levels are also presented. This will be realized with the software Python on a Raspberry Pi. The project will be produced in approximately one month and will be evaluated on the following six criteria

[^1]: Industries, Adafruit. “DHT11 Basic Temperature-Humidity Sensor + Extras.” Adafruit Industries Blog RSS, https://www.adafruit.com/product/386. 
[^2]: Nelson, Carter. “Modern Replacements for DHT11 and dht22 Sensors.” Adafruit Learning System, https://learn.adafruit.com/modern-replacements-for-dht11-dht22-sensors/what-are-better-alternatives.   
[^3]:“How to Connect dht11 Sensor with Arduino Uno.” Arduino Project Hub, https://create.arduino.cc/projecthub/pibots555/how-to-connect-dht11-sensor-with-arduino-uno-f4d239.  
[^4]:Team, The Arduino. “What Is Arduino?: Arduino Documentation.” Arduino Documentation | Arduino Documentation, https://docs.arduino.cc/learn/starting-guide/whats-arduino.  

## Success Criteria

1. The solution provides a visual representation of the Humidity and Temperature values inside a dormitory (Local) and outside the house (Remote) for a period of minimum 48 hours. 
1. ```[HL]``` The local variables will be measure using a set of 4 sensors around the dormitory.
2. The solution provides a mathematical modelling for the Humidity and Temperature levels for each Local and Remote locations. ```(SL: linear model)```, ```(HL: non-lineal model)```
3. The solution provides a comparative analysis for the Humidity and Temperature levels for each Local and Remote locations including mean, standad deviation, minimum, maximum, and median.
4. ```(SL)```The Local samples are stored in a csv file and ```(HL)``` posted to the remote server.
5. Create a prediction the subsequent 12 hours for both temperature and humidity.
6. A poster summarizing the visual representations, model and analysis is created and communicated.

# Criteria B: Design

### System Diagram **HL**

![](sysdim_hl.png)

**Fig.2** shows the system diagram for the proposed solution (**HL**). The indoor variables will be measured using a Raspberry PI and four DHT11 sensors located inside a room. Four sensors are used to determine more precisely the physical values and include measurement uncertainty. The outdoor variables will be requested to the remote server using a GET request to the API of the server at ```192.168.6.147/readings```. The local values are stored in a CSV database locally and POST to the server using the API and TOKEN authentication. A laptop computer is used for remotely controlling the local Rasberry Pi using a Dekptop sharing application (VNC Viewer). (Optional) Data from the local raspberry is downloaded to the laptop for analysis and processing.


### Record of Tasks
| Task No | Planned Action                                                | Planned Outcome                                                                                                 | Time estimate | Target completion date | Criterion |
|---------|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------|------------------------|-----------|
|       | meet with client　  | Talk with the client to dicuss the problems they are facing and brainstorm solutions to create a plan to help the client resolve the problems　|  15min | Nov 22| A
|       |Brainstorm and write the problem definition| Both write problem definition and organize files for this program in githab| 30min| Nov 22 |B
|       | Wirte Design statement | A clear outline of the final goal of the project and the components to be completed | 60min |Nov 23
|       | Gathering materials and assigning tasks to the scope of work |Procure the materials needed to build the equipment to measure temperature and humidity in the dormitory and bring the materials back home with the sole intention of building a weather station for the client  | 60min |Nov
|       |Write the Problem context             |we understood how the code works          |  10m in          |  Nov 24         | A 
|       |research about raspberry pi                      |research about raspberry pi features and benefits and what can be implemented          |  25min         |  Nov 29         | A
|        |Write code for program                           |  We wrote code so that the sensor could periodically measure humidity and temperature.        |  45min          |  Nov 30         | A
|    |We wired the raspberry pi, sensors and raspberry pi| Using a breadboard, I was able to wire accurately | 45min | Nov 31| A    
|    |Create a system that "uploads the obtained data to the server |      |  120min  | Dec 6 |B

## Test Plan

# Criteria C: Development

### List of techniques used

### Development
### MVP-Minimum Viable Product
As a prototype for a method of measuring and collecting temperature and humidity data, we have created MVP, which runs in Python code on a Raspberry Pi connected to a single DHT sensor. This code allows the Raspberry Pi to read a set of temperature and humidity data from the DHT sensor and display it as output on the terminal. For more information, see the Python code below.


```.py
    
def sensor(a):
    today = datetime.datetime.now()
    DHT_SENSOR = Adafruit_DHT.DHT11
    DHT_PIN = a
    humidity,temperature = Adafruit_DHT.read(DHT_SENSOR,DHT_PIN)
  　　　　while humidity == None or temperature == None:
        humidity,temperature = Adafruit_DHT.read(DHT_SENSOR,DHT_PIN)
 
```
### Server initialization
Logging in, registering and creating 8 sensors in the server. Code is as below:
```.py
import requests

'''
new_user = {'username': 'masamu','password':'123'}
req = requests.post('http://192.168.6.142/register',json = new_user)
print(req.json())
'''

user = {'username': 'masamu','password':'123'}
req = requests.post('http://192.168.6.142/login',json = user)
access_token = req.json()['access_token']
print(req.json())


'''auth = {"Authorization": f"Bearer {access_token}"}

count = 0
for i in range(1,9):
    if i >= 5:
        type = 'Temperature'
        unit = 'C'
    else:
        type = 'Humidity'
        unit = '%'
    sensorname = f'sensor_masagen_{type}_{i}'
    print(i,type,sensorname)
    new_sensor ={ "type": type,"location": "R2-12A", "name": sensorname,"unit":unit }
    r = requests.post('http://192.168.6.142/sensor/new', json=new_sensor, headers=auth)
    print(r.json())'''


auth = {"Authorization": f"Bearer {access_token}"}
'''
new_sensor ={ "type": 'Temperature',"location": "R2-12A", "name": 'masamu_test',"unit":'C' }
r = requests.post('http://192.168.6.142/sensor/new', json=new_sensor, headers=auth)
print(r.json())
'''
r = requests.get('http://192.168.6.142/sensors')
print(r.json()['readings'])
for i in r.json()['readings'][0]:
    if i['owner_id'] == 10:
        print(i)


r = requests.get('http://192.168.6.142/user/readings', headers=auth)
print(r.json())
for i in r.json():
    print(i)

```
# Criteria D: Functionality

A 7 min video demonstrating the proposed solution with narration
