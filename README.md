# iot
1
AIM: Study of Arduino board and Interfacing of LED (s) with Arduino.
¬¬Code:
int led = 12; void setup() 
{ 
// put your setup code here	pinMode(led, OUTPUT); 
} 
void loop() { 
// put your main code here, to run repeatedly: digitalWrite(led,HIGH); 
delay(300); 
digitalWrite(led,LOW); 
delay(100); 
} 

Output:
![image](https://user-images.githubusercontent.com/132896743/236797552-4a6435d0-1914-4557-a2eb-58f1ba02302c.png)



Practical 2
AIM: Study and implementation of Buzzer, Switches, LCD, keypad, LDR, Ultrasonic sensors and PWM interfacing with Arduino. 
1)	Buzzers
Code:
int led =12; 
int btn=6; 
int state=HIGH;
void setup() { 
	// put your setup code here, to 
	run once: pinMode(led, OUTPUT);
	pinMode(btn, INPUT); 
} 
void loop() { 
// put your main code here, to run repeatedly: 
int reading=digitalRead(btn);
if(reading!=state){ 
	state=!state; 
	digitalWrite(led,state); 
	} }
![image](https://user-images.githubusercontent.com/132896743/236797653-fb52e960-3682-4d87-8189-57f398e4165c.png)



2)	Switches

Code: 

int led=12; 
int btn=6; 
int reading;   
int state=LOW; 
int last_state=LOW; 
void setup(){ 
 // put your setup code here,to run once: 
pinMode(led,OUTPUT); 
pinMode(btn, INPUT); 
} 
void loop() { 
// put your main code here, to run repeatedly: 
int reading=digitalRead(btn); 
if(reading==HIGH){ 
if(last_state==HIGH){ 
state=!last_state; 
digitalWrite(led, last_state); 
    } 
} 
else{ 
last_state=!last_state; 
digitalWrite(led,last_st ate); 
    }
 }

Output:
![image](https://user-images.githubusercontent.com/132896743/236797794-ba2dfb42-7cbe-4d76-a187-f82201bb69ae.png)





3)	LCD
![image](https://user-images.githubusercontent.com/132896743/236797890-bef53582-7283-4eb1-9960-1df397a5c676.png)

Code: 
#include <LiquidCrystal.h> 
LiquidCrystal lcd(13,12,6,4,3,2); 
void setup() { 
	// put your setup code here, t0 run once: 
	lcd.begin(16,2); 
} 
void loop() { 
	// put your main code here, to run repeatedly: 
	lcd.setCursor(0,0); 
lcd.print("12345"); 
}

Output: 
![image](https://user-images.githubusercontent.com/132896743/236797949-a961b333-2dde-4efb-9cd3-e3b3782428a5.png)





4)	Keypad:
Code:
#include <Keypad.h> 
const byte 
ROWS = 4; 
const byte COLS = 4; 
char keys[ROWS][COLS] = { 
	{'1','2','3','A'}, 
	{'4','5','6','B'}, 
	{'7','8','9','C'}, 
	{'*','0','#','D'},
}; 
byte rowPins[ROWS] = {9, 8, 7, 6}; 
byte colPins[COLS] = {5, 4, 3, 2}; 
Keypad keypad = Keypad( makeKeymap(keys), rowPins, colPins, ROWS, COLS ); 

void setup(){ 
	serial.begin(9600); 
} 
void loop(){ 
	char key = keypad.getKey(); 
	if (key){ 
	Serial.print("Key Pressed : "); 
	Serial.println(key); 
	} 
}  

Output:
![image](https://user-images.githubusercontent.com/132896743/236798032-d57f1444-aabc-4bbb-b66e-71e212ead15f.png)



5)	LDR
Code:
#include LiquidCrystal_I2C.h> 
#define LDR_PIN 2 

const float RL10 = 50; 
LiquidCrystal_I2C lcd(0x27, 20, 4); 

void setup() { 
	pinMode(LDR_PIN, INPUT); 
	lcd.init(); 
	lcd.backlig ht(); 
} 
void loop() { 
	int analogValue = analogRead(A0); 
	float voltage = analogValue / 1024. * 5; 
	float resistance = 2000 * voltage / (1 - voltage / 5); 
	float lux = pow(RL10 * 1e3 * pow(10, GAMMA) / resistance, (1 / GAMMA)); 
 
lcd.setCursor(2, 0); 
lcd.print("Room: "); 
if (lux > 50) { 
		lcd.print("Light!"); 
} 
else { 
	lcd.print("Dar k "); 
} 
lcd.setCursor( 0, 1); 
lcd.print("Lux: "); 
lcd.print(lux); 
lcd.print(" "); 
delay(100);
}


 Output:
 ![image](https://user-images.githubusercontent.com/132896743/236798135-2241471f-d96e-41ba-8676-30d8a22c5289.png)





6)	Ultrasonic Sensor
Code: 
#define echoPin 6 
#define triggerPin 7 
 
void setup() { 
	pinMode(triggerPin, OUTPUT); 
	pinMode(echoPin, INPUT); 
	Serial.begin(9600); 
	Serial.println("Ultrasonic Sensor HCSR04 Test"); 
	Serial.println("with Arduino UNO"); 
} 
void loop() { 
	long highPulseDuration; 
	int calculatedDistance Cm;  
	digitalWrite(triggerPin, LOW); 
	delayMicroseconds(5); 
	digitalWrite(triggerPin, HIGH); 
	delayMicroseconds(10); 
	digitalWrite(triggerPin, LOW); 
	highPulseDuration = pulseIn(echoPin, HIGH); 
	calculatedDistanceCm = highPulseDuration * 0.034 / 2; 
 
	Serial.print("Calculated Distance: "); 
	Serial.print(calculatedDista nceCm); 	
	Serial.println("cm"); 
}


Output:
![image](https://user-images.githubusercontent.com/132896743/236798206-1a38e58c-69ba-4139-ae27-1e049fe12fbf.png)





Practical 3
AIM: Study of serial communication and device control using serial communication with Arduino.
Example:
In this example, we will send a string from Arduino to PC. Once we upload the sketch into Arduino. We will see this string will be printing on Serial Monitor Window of Arduino IDE. 
void setup() { 
	Serial.begin(9600); 
} 
void loop() { 
	Serial.println("Hello om Umesh"); 
	delay(1000); 
}

Hardware Setup: We only need to connect Arduino Uno to PC over standard USB Cable. Once we have done connection we are ready to upload the sketch to Arduino and open serial monitor window to display data sent from Arduino. As we been transmitting string from Arduino to PC. We will observe that LED connected to TX Pin on Arduino will light up. 

![image](https://user-images.githubusercontent.com/132896743/236798307-40ade6cf-627e-469f-acd8-b105dedfe145.png)


![image](https://user-images.githubusercontent.com/132896743/236798332-b457b6b8-bfc9-47ff-801e-716a1283e9af.png)


![image](https://user-images.githubusercontent.com/132896743/236798369-8d88c964-a6cc-4e76-a169-59641c369fe7.png)



Practical 4
AIM: Study and implementation LED (s) Interfacing with NodeMCU.
NodeMCU
NodeMCU is an open-source LUA based firmware developed for the ESP8266 wifi chip. By exploring functionality with the ESP8266 chip, NodeMCU firmware comes with the ESP8266 Development board/kit i.e. NodeMCU Development board.

NodeMCU Dev Kit/board consist of ESP8266 wifi enabled chip. The ESP8266 is a low-cost Wi-Fi chip developed by Espressif Systems with TCP/IP protocol. For more information about ESP8266, you can refer to the ESP8266 WiFi Module.
NodeMCU Dev Kit has Arduino like Analog (i.e. A0) and Digital (D0-D8) pins on its board.

![image](https://user-images.githubusercontent.com/132896743/236798431-6c82730d-d65f-4cae-a8fa-17a41878e8b1.png)


Code:
int val = 0 ; 
void setup(){ 
	Serial.begin(9600); 
	// sensor buart rate 
	pinMode(5,HIGH); 
	// D5 PIN FOR LED 
} 

void loop(){ 
val = digitalRead(4);  // Push Button output pin connected D1 
Serial.println(val); // see the value in serial m0nitor in Arduino IDE 
delay(100); // for timer 

if(val == 1 ){ 
	digitalWrite(5,HIGH); // LED ON 
} 
else { 
	digitalWrite(5,LOW); // LED OFF 
     } 
}


#img





Practical 5
AIM: Implementation of Publishing data on ThingSpeak cloud.
Code:
#include <WiFi.h> 
#include <ThingSpeak.h> // always include thingspeak header file after other header files and custom macros 
 
#define SECRET_SSID "Wokwi-GUEST" // replace with your WiFi network name 
#define SECRET_PASS "" // replace with your WiFi password 
 
#define SECRET_CH_ID 2015326   // replace 0000000 with your channel number 
#define SECRET_WRITE_APIKEY "15TYOGZIQ0EHI2YQ"  // replace XYZ with your channel write API Key 
 
char ssid[] = SECRET_SSID;   // your network SSID (name)  
char pass[] = SECRET_PASS;   // your network password 
int keyIndex = 0;            // your network key Index number (needed only for WEP) 

WiFiClient  client; 
unsigned long myChannelNumber = SECRET_CH_ID; 
const char * myWriteAPIKey = SECRET_WRITE_APIKEY; 
int temppin=32; 
float pinval; 
float temp=0.00; 
void setup()  
{ 
  pinMode(temppin,INPUT); 
  Serial.begin(115200);  //Initialize serial   
  while (!Serial) { 
    ; // wait for serial port to connect. Needed for Leonardo native USB port only 
  } 
  WiFi.mode(WIFI_STA);    
  ThingSpeak.begin(client);  // Initialize ThingSpeak 
} 
void loop()  
{ 
  // Connect or reconnect to WiFi   
  if(WiFi.status() != WL_CONNECTED) { 
	Serial.print("Attempting to connect to SSID: ");     
	Serial.println(SECRET_SSID);     
	while(WiFi.status() != WL_CONNECTED) { 
	WiFi.begin(ssid, pass); // Connect to WPA/WPA2 network. Change this  line if using open or WEP network 
        Serial.print("."); 
	delay(5000);      
    }  
    Serial.println("\nConnected."); 
  } 	
	pinval=analogRead(temppin);   
	temp=pinval*(0.122); 
	Serial.println(temp); 
	// Write to ThingSpeak. There are up to 8 fields in a channel, allowing you to store up to 8 different 
	// pieces of information in a channel.  Here, we write to field 1. 
	int x = ThingSpeak.writeField(myChannelNumber, 1, temp, myWriteAPIKey);   
	if(x == 200) { 
		Serial.println("Channel update successful."); 
  	} 
  	else 
  	{ 
    		Serial.println("Problem updating channel. HTTP error code " + String(x)); 
  	} 
  delay(1000); // Wait 7 seconds to update the channel again 
}

Output:
![image](https://user-images.githubusercontent.com/132896743/236798704-74917243-27c1-493e-8acc-1f6b7c6114ed.png)






Practical 6
AIM: Controlling Appliances using NodeMCU MQTT over the Internet. (Adafruit Cloud).

MQTT 
MQTT, also known as Message Queuing Telemetry Transport, is a protocol that uses a publish and subscribe paradigm. It is simple, lightweight, and it gives you the luxury to stay connected to your devices the entire time. 
Moreover, MQTT works on top of any wireless technology. You can use it with TCP/IP, Zigbee, Bluetooth, and many more. You name it. 
Before we proceed, you need to learn these terms first: 
•	Broker – The server that distributes the data to the interested clients. 
•	Client – A device that sends or receives information via the broker. 
•	Topic – A feed of data that a broker manages. Clients can publish, subscribe, or do both to a topic. 
•	Publish – A client sends information to a topic. 
•	Subscribe – A client tells the broker which topics it is interested in. 
•	QoS – QoS stands for Quality of Service. It represents the level of connection between a client and a broker. 
o	0, also known as at most once, is the lowest QOS. The broker does not acknowledge the delivery and the client does not retransmit. 
o	1, also known as at least once, the client continuously transmits the data until an acknowledgment from the broker is received. 
o	2, also known as exactly once, is the highest QOS. It is the safest but also the slowest level. It uses a 4-way handshake method. 

How MQTT Works 


![image](https://user-images.githubusercontent.com/132896743/236799426-43d300f0-8cc1-404e-b233-b80b45cbc3a3.png)



To demonstrate, suppose we have 3 clients and Adafruit IO as a broker. Client 1 is connected to a temperature and humidity sensor, Client 2 is connected to a Humidifier, and Client 3 is connected to an Air Conditioner. 


In this case, the topics are Room Temperature and Humidity and Aircon Relay. Client 1 publishes data into Room Temperature and Humidity. Since Client 2 and Client 3 are subscribed to the topic, the broker distributes the data to them. Client 2 opens the humidifier when the topic tells that the air is dry while Client 3 opens the Air Conditioner when the topic tells that it is warm. Moreover, Client 3 is subscribed to the topic of Aircon Relay as well. When the topic tells that the aircon is on, Client 2 opens the humidifier. 
A broker just acts as a tollway for data. It doesn’t send commands to the clients. It only directs the data the client is interested in. 
Meanwhile, clients aren’t really connected to anything other than the broker. Clients can go to deep sleep or completely shut down to conserve power without affecting the connection of the MQTT system. 
Now that we understand the theory, let’s proceed by setting up an MQTT broker on Adafruit IO. 

Setting up MQTT on Adafruit IO 
First, go to https://io.adafruit.com/ and create an account. Once logged in, go to the home page. Under Actions, select Create a New Dashboard. 

![image](https://user-images.githubusercontent.com/132896743/236799521-3244f1cd-2126-4235-9688-de7c713b3000.png)


Then, click create after giving the dashboard a name and a short description. 


![image](https://user-images.githubusercontent.com/132896743/236799592-a074c053-1173-4ffb-9f4e-487541ebd69a.png)


Next, go to your new Dashboard. 


![image](https://user-images.githubusercontent.com/132896743/236799656-6516b115-4602-4bef-b6d7-94bd70f24d47.png)



As you can see, the dashboard is still empty. You should populate it first by creating a new block. In order to do that, press the blue plus button on the right side of the dashboard. 
 
Blocks are switches, buttons, levers, gauges, and more visualization techniques that represent and react to your data. For our sample project, we need 2 gauges to display the room’s temperature and humidity and a switch to toggle an LED. 
After selecting a block, Adafruit IO prompts you to choose a feed. Feeds can also be called MQTT topics. We need 3 feeds to hold the temperature and humidity values of the DHT sensor, and the status of the LED. Create a feed using the create button on the right. 

![image](https://user-images.githubusercontent.com/132896743/236799737-ea70e4f4-f48c-4bca-857b-56b8fce40909.png)


	Next, configure the block settings as shown below. 
	
![image](https://user-images.githubusercontent.com/132896743/236799799-20589ccb-0273-460b-8cd7-35937580e5a2.png)



	







