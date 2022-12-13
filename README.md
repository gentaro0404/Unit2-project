![gachapin.jpeg](gachapin.jpeg)
*Post, The Huffington. “ガチャピン、放送事故で透明に。松雪彩花アナのフォローに「神対応」の声.” ハフポスト, ハフポスト, 5 Feb. 2016, https://www.huffingtonpost.jp/2016/02/05/gachapin-weathernews_n_9173020.html.*

**Fig.1**Japanese green mascot character looks assimilated into the green background[^0]


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


## How data is stored
We stored the temperature and humidity data  in both seperate database csv files, and sent the datas to the sensors created in the server everytime the set of data is collected

## Flow Diagram 1 - Main File
![project_main_flow.jpg](project_main_flow.jpg)
**Fig.3** shows the flow diagram of the main file that collects datas from the server and stores them into csv files and sends them to the server.

## Flow Diagram 2 - Server Creation
![project_server_flow.jpg](project_server_flow.jpg)
**Fig.4** shows the flow diagram of the initiation of accounts for the servers and sensors.

## Flow Diagram 3 - MVP
![project_MVP_flow.jpg](project_MVP_flow.jpg)
**Fig.5** shows the flow diagrams for the minimum viable product for the project.

### Record of Tasks
| Task No | Planned Action                                                | Planned Outcome                                                                                                 | Time estimate | Target completion date | Criterion |
|---------|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------|------------------------|-----------|
|    1   | meet with client　  | Talk with the client to dicuss the problems they are facing and brainstorm solutions to create a plan to help the client resolve the problems　|  15min | Nov 22| A|
| 2    |Brainstorm and write the problem definition| Both write problem definition and organize files for this program in githab| 30min| Nov 22 |B|
|  3     | Wirte Design statement | A clear outline of the final goal of the project and the components to be completed | 60min |Nov 23||
|  4     | Gathering materials and assigning tasks to the scope of work |Procure the materials needed to build the equipment to measure temperature and humidity in the dormitory and bring the materials back home with the sole intention of building a weather station for the client  | 60min |Nov||
|   5   |Write the Problem context             |we understood how the code works          |  10min          |  Nov 24         | A |
|   6    |research about raspberry pi                      |research about raspberry pi features and benefits and what can be implemented          |  25min         |  Nov 29         | A|
|   7   |Write code for program                           |  We wrote code so that the sensor could periodically measure humidity and temperature.        |  45min          |  Nov 30         | A |
|  8 |Test run for sensor |Write and run a code that measures once every 5 seconds for testing.| 60min | Nov 30| A|
|  9  |We wired the raspberry pi, sensors and raspberry pi| Using a breadboard, I was able to wire accurately | 45min | Nov 30| A |
|  10  |Connect raspberry pi to computer and test run of sensors. | Check that the connection between the sensor and the Raspberry Pi is made properly. Complete the temporary assembly of the device. | 80 min | Dec 1 | A|
|  11  |Create MVP | After confirming that the basic structure and function of the product is working properly, we move on to the final finished product. | 80 min | B||
|  12  |  Register user to server and obtain access code. | Create a user with a secure username and password to access the server. Obtain an access code to log in to the server and be able to post | 70min | Dec 1 | C|
|  13  |We wired the raspberry pi, sensors and raspberry pi| Using a breadboard, I was able to wire accurately | 45min | Dec 1| A|
|  14  | Make cron tab |This is to ensure that DHT's sensors send data to the computer at 5 minute intervals.	| 45 min | Dec 1 |C|
|   15 |Create a system that "uploads the obtained data to the server | Transmits humidity and temperature data to server every 5 minutesv    |  120min  | Dec 3 |B|
|  16 |Run code for 48 hours in order to collect temperature and humidity data in R2-12 A.| Take R2-12A humidity and temperature data at 5-minute intervals for 48 hours.| 48 hrs |Dec 3-5 |C|
| 17 |Unexplained trouble, code stops.And fixed|It was discovered that the WIfi connection had been lost in the process. Additional necessary tools were installed to solve the problem.|  210 min |Dec 6 |B|
| 18  | Draw 3 flow diagrams of aspects of code.　| I drew FLOW diagrams for the MVP, the server code, and the overall code. | 200min | Dec 7 |A|
| 19 | Find out the appropriate temperature and humidity for human living | To obtain criteria for determining appropriate/inappropriate humidity and temperature levels on the UWC ISAK campus | 30 min |Dec 7 | B|
| 20 |Collect data from outdoor sensors|To compare outdoor indoor temperature changes from the posted data. |    180 min | Dec 7 | A|
| 21 | Create coding to graph school and room temperature and humidity data | Create a scatter plot graph using a nonlinear best-fit function|110 min | Dec 8 | B|
| 22 |Pilot graphing of data | Use outdoor data and apply it to the code you have created. | 50 min | Dec 8 | A|
| 23 |Coding prototype graphing for one specific data | When plotting graphs from all sensors and the average of one specific set of data (room temperature)| 80 min | Dec 9 | B|
| 24  |Outline video outlines, summarize data and images, and present the final product/solution.| Gather all information necessary to create an organized video to showcase the product. | 80 min | Dec 9 | B|
| 25 | Find out how to write a science poster | Research to write to cover the Criteria | 50 min | Dec 10 |A|
|26 | Update show your CT | To increase the thinking power of the computer by updating pattern recognition and decomposition | 30 min | Dec 13 |B|
| 27| Create scientific poster | To clearly present the background information, methodologies, materials, results, analysis and conclusion for the client. | 80 min | Dec 11-13 |B|
|28 | Video Creation | Demonstrate how the finished product works, explain how the product met the success criteria, and clearly describe the project. | 40 min | Dec 13 |A|
|29 | Finish updating project repository | Cover all the essentials and do it by the submission deadline | 50 min | Dec 13 |A|


## Test Plan
| Software Test Type | Input | Process | Planned Output  |
|------|-------------|:---------|:--------|
| Integration Testing | Raspberry Pi and VNC Viewer | Download Raspberry Pi, VNC Viewer, vnc viewer, enter the address of the raspberry pi in the vnc viewer, access the raspberry pi using the username and password from the VNC viewer. | Authenticate the user name and password in the VNC viewer to be able to connect remotely to the Raspberry Pi. |
| Unit Testing | Code to receive information from DHT sensor | Run code and wait for output from DHT sensor. | Verify that the DHT sensor is functioning properly.|
| Unit testing | Code to obetain data from DHT11s (MVP) | Run code and Input pin number odf senser(4,17,22,27)when primopted by program | program will print if the sensor is working , and if the sensor is working, the data from the sensor to the terminal|
| Performance   Testing | MVP code | Run code and Input PIN number of sensor(4,17,22,27)when prompted by program and Measure time until output is printed on the the terminal | Code will collect data and desply an output on the termrinal in 5 seconds |
| Integration Testing | Bash program and Main program | Run code and Wait and see if data is being added to the JSON file every minutes. | Temperature and humiditiy data from all four sensors should be appended to the same JSON file with datatime |
| Unit  Testing | Code for writing to JSON files | Run code | Date wil collected from sensors and formatted and finally inserted into the JSON file along with the date time and sensor_id |
| Unit Testing | Graphing Code | Run code and wait for graph to appear and Reference JSON file to compare accuracy of data | Graph and respective statistics should line up with data from JSON file |
 

# Criteria C: Development

### List of techniques used
| Technique |
|-----------|
| Posting to a remote server with server API. |
| Retrieving data from a remote server with server API and requests library. |
| For loops in order to run code under certain conditions. For example, to get readings for multiple DHT11 sensors with one for loop of code. Utilizing a for loop is more efficient than creating a code for each sensor separately. |
| Creating lists (in order to save data from DHT11 sensors by temperature and humidity). |
| Creating CSV files (in order to save data from DHT11 sensors by temperature and humidity). |
| Plot median, mean, maximum, minimum, standard deviation and a non linear model using python. |
| Predicting temperature and humidity values based on line of best fit equation (non linear model). |
| Smoothing data on a graph. |

### Existing tools:

| Software/development tools | coding structure tools |  Libraries   |
| :------------------------: | :--------------------: | :----------: |
|       Python/Pycharm       |       for loops        |   datetime   |
|         VNC viewer         |      API requests      |   requests   |
|                            |                        |     csv      |
|                            |                        | Adafruit_DHT |
|                            |                        |  matplotlib  |
|                            |                        |    numpy     |

## Computational Thinking

#### Decomposition

Decomposition is the process of breaking a task into smaller, tractable problems. In the Project 2 code, the skill of decomposition can always be seen at large and small scales.

### Main File
```.py
import requests
import Adafruit_DHT
import datetime
import time

user = {'username': 'masamu','password':'123'}
req = requests.post('http://192.168.6.142/login',json = user)
access_token = req.json()['access_token']
print(req.json())
auth = {"Authorization": f"Bearer {access_token}"}

def convert(a):
    if a == 2:
        return 0
    if a == 3:
        return 1
    if a == 4:
        return 2
    if a == 17:
        return 3
    
    
def sensor(a):
    today = datetime.datetime.now()
    DHT_SENSOR = Adafruit_DHT.DHT11
    DHT_PIN = a
    humidity,temperature = Adafruit_DHT.read(DHT_SENSOR,DHT_PIN)
    while humidity == 'null' or temperature == 'null':
        humidity,temperature = Adafruit_DHT.read(DHT_SENSOR,DHT_PIN)
    
    new_record ={"datetime":str(datetime.datetime.now()),"sensor_id":472 + convert(a), "value":humidity}
    r = requests.post('http://192.168.6.142/reading/new', json=new_record, headers=auth)
    
    print(r.json())
    new_record ={"datetime":str(datetime.datetime.now()),"sensor_id":476 + convert(a), "value":temperature}
    r = requests.post('http://192.168.6.142/reading/new', json=new_record, headers=auth)
    print(r.json())

    
#    time.sleep(1)



for i in range(0,172801,300):
    sensor(2)
    sensor(3)
    sensor(4)
    sensor(17)
    time.sleep(300)
```

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
## Ouｔside deta
Create two lists from the raw data, retrieve the data from the school's server, split the data into dictionary temperature and humidity, and retrieve the average, minimum, maximum, and median of humidity and temperature levels from the dictionary.


```.py
from matplotlib import pyplot as plt
import requests
import math
import numpy as np


req = requests.get('http://192.168.6.142/readings')
data = req.json()
readings = data["readings"][0]
temp = []
hum = []
count = 0
print('succesful')
for i in readings:
    if i['sensor_id'] == 4:
        hum.append(i)
    if i['sensor_id'] == 5:
        temp.append(i)
#        count +=1

data = {'temp': temp[-576:], 'hum': hum[-576:]}
value = {'temp': [], 'hum': []}

for i in data['temp']:
    value['temp'].append(i['value'])
for i in data['hum']:
    value['hum'].append(i['value'])
print(value)


def mean(a):
    sum = 0
    for i in value[str(a)]:
        sum += i
    mean = round(sum/len(value[str(a)]),1)
    print(f'mean of {a}: {mean}')
    sumdiv = 0
    for i in value[str(a)]:
        sumdiv += (i - mean)**2
    standad_deviation = math.sqrt(sumdiv/len(value[str(a)]))
    print(f'standad deviation of {a}: {round(standad_deviation,2)}')
mean('temp')
mean('hum')

print()

def min(a):
    min = 50
    for i in value[str(a)]:
        if i < min:
            min = i
    print(f'minimum value of {a}: {min}')
min('temp')
min('hum')

def max(a):
    max = 0
    for i in value[str(a)]:
        if i > max:
            max = i
    print(f'maximum value of {a}: {max}')
max('temp')
max('hum')

def median(a):
    median = sorted(value[str(a)])
    print(f'the median of {a}: {median[288]}')
median('temp')
median('hum')



def plot(a):
    z = []
    zy = []
    for i in range(0, len(value[str(a)])):
        z.append(i)
    print(z)
    if a == 'temp':
        c = 'r'
    elif a == 'hum':
        c = 'b'
    plt.plot(value[str(a)],color = c)
    m,b,o,k = np.polyfit(z,value[str(a)], 3)
    for i in range(len(z)):
        zy.append(m*i**3+b*i**2+o*i**1+k)
    plt.plot(zy)
    pre_x = []
    pre_y = []
    for i in range(576,570+12*12):
        pre_x.append(i)
    for i in pre_x:
        pre_y.append(m*i**3+b*i**2+o*i**1+k)
    plt.plot(pre_x,pre_y)
    print(m,b,o,k)


plot('temp')
plot('hum')
plt.ylabel('red = tempareture(C)\nblue = humidity(%)')
plt.title('outdoor data')
plt.show()
```
### Raw data
Derived from data, statistical data
```.py
mean of temp: 24.6

standad deviation of temp: 2.02

mean of hum: 26.7

standad deviation of hum: 4.58

minimum value of temp: 18.0

minimum value of hum: 20.0

maximum value of temp: 29.0

maximum value of hum: 44.0

the median of temp: 25.0

the median of hum: 25.0

the equasion for the graph and prediction: ax^3 + bx^2 + cx + d

a= 1.1560766498859011e-07 b= -0.0001567440266767569 c= 0.0528467669108278 d= 21.234353936698792

a= -2.0075182536069003e-07 b= 0.00032877661011873274 c= -0.12436927725233127 d= 35.786378839051544
```

![outdoordata.png](outdoordata.png)
**Fig.6** 
Graph of average, minimum, maximum, and median outdoor humidity and temperature

## Indoor data
From the raw data, we created two dictionaries, one for "temperature" and one for "humidity". For each, we included data from four sensors. The dictionary of values then finds the average of the data from the four sensors. Then, from the data, the levels of Local, Humidity and Temperature are obtained with mean, standard deviation, minimum, maximum and median.

```.py
from matplotlib import pyplot as plt
import requests
import math
import datetime
import time

user = {'username': 'masamu','password':'123'}
req = requests.post('http://192.168.6.142/login',json = user)
access_token = req.json()['access_token']
#print(req.json())
auth = {"Authorization": f"Bearer {access_token}"}

r = requests.get('http://192.168.6.142/user/readings', headers=auth)

#print(len(r.json())/6)
value_temp = {'t1':[],'t2':[],'t3':[],'t4':[]}
value_hum = {'h1':[],'h2':[],'h3':[],'h4':[]}

for i in r.json():
    if int(i['id']) >0:
        if int(i['sensor_id']) == 472:
            value_hum['h1'].append(i['value'])
        elif int(i['sensor_id']) == 473:
            value_hum['h2'].append(i['value'])
        elif int(i['sensor_id']) == 474:
            value_hum['h3'].append(i['value'])
        elif int(i['sensor_id']) == 475:
            value_hum['h4'].append(i['value'])
        elif int(i['sensor_id']) == 476:
            value_temp['t1'].append(i['value'])
        elif int(i['sensor_id']) == 477:
            value_temp['t2'].append(i['value'])
        elif int(i['sensor_id']) == 478:
            value_temp['t3'].append(i['value'])
        elif int(i['sensor_id']) == 479:
            value_temp['t4'].append(i['value'])

for i in value_temp:
    value_temp[str(i)] = value_temp[str(i)][-576:]
for i in value_hum:
    value_hum[str(i)] = value_hum[str(i)][-576:]

print(value_hum)
print(value_temp)
ave = {'temp':[],'hum':[]}


for i in range(0,576):
    sum = 0
    for x in value_temp:
        sum += value_temp[x][i]
    ave['temp'].append(round(sum/4,2))
for i in range(0, 576):
    sum = 0
    for x in value_hum:
        sum += value_hum[x][i]
    ave['hum'].append(round(sum / 4, 2))
print(ave)

def plot_ave():
    for i in ave:
        plt.plot(ave[str(i)])
        plt.title(f'average {str(i)}')
        plt.show()
plot_ave()

def mean():
    for i in ave:
        sum = 0
        for x in ave[i]:
            sum += x
        mean = sum/len(ave[i])
        print(f'the average of {i} is {mean}')
    sumdiv = 0
    for i in ave:
        sumdiv += (i - mean) ** 2
        standad_deviation = math.sqrt(sumdiv / len(i))
    print(f'the standad deviation of {i} is {standad_deviation}')
mean()

def min():
    for i in ave:
        min = 50
        for x in ave[i]:
            if x < min:
                min = x
        print(f'the minimum value of {i} is {min}')
min()

def max():
    for i in ave:
        max = 0
        for x in ave[i]:
            if x > max:
                max = x
        print(f'the maximum value of {i} is {max}')
max()

def median():
    for i in ave:
        median = sorted(i)
        print(f'the median of {i} is {median[288]}')
median()

def graph(a):
    for i in a:
        plt.plot(a[str(i)])
    plt.title('temperature for each sensor')
    plt.ylabel('temperature(C)')
    plt.show()
graph(value_temp)
```

### Raw data
Derived from data, statistical data
```.py
the average of temp is 24.6875
the average of hum is 21.786024305555557
the standad deviation of average hum is 82.452322081714
the minimum value of average temp is 18.5
the minimum value of average hum is 20.0
the maximum value of average temp is 28.0
the maximum value of average hum is 52.0
the median of average temp is 25.0
the median of average hum is 20.0
function for t1
-1.3366302570644902e-07 0.00013040309800325963 -0.02947645666034394 25.263200665509498

function for t2
-1.4960101604489952e-07 0.00014012467054260225 -0.03003877805614878 25.241554162508606

function for t3
-1.2605386785874063e-07 0.00011463948793833798 -0.021809425632876692 24.065657445186066

function for t4
-1.8524444141981163e-07 0.00015913163539969327 -0.03046560323093323 24.587966351823543

function for h1
1.590675798723074e-07 -0.00017329649078573966 0.048258985284268356 19.884673144319873

function for h2
1.799170895239079e-07 -0.0001606946446169988 0.039072404116739734 18.943481157589392

function for h3
-7.804013933912029e-08 0.00010278678629683801 -0.03177265137300652 22.680720274635206

function for h4
1.4753813620259307e-07 -7.08959508039189e-05 0.014504431361656557 19.36712353683
```

![average_hum.JPG](average_hum.JPG)

**Fig.7** 
Humidity averaged from four sensors
![average_temp.JPG](average_temp.JPG)

**Fig.8** 
Temperature averaged from four sensors

![temperature_for_each_sensor.JPG](temperature_for_each_sensor.JPG)

**Fig.9** 
temperature averaged from each of the four sensors for 48 hours and the forecast for the next 12 hours
![humidity_for_each_sensor.JPG](humidity_for_each_sensor.JPG)

**Fig.10** 
humidity obtained from the average value of each of the four sensors for 48 hours and the forecast for the next 12 hours.

# Criteria D: Functionality

A 7 min video demonstrating the proposed solution with narration
