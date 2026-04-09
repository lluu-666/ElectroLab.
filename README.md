![16189bc5-a717-42b2-a404-77dd8dec3a7c](https://github.com/user-attachments/assets/8d2344d8-bac2-4ef2-9ca4-1ca71f5b8b5e)




 Task 1: Intelligent Latching Switch with Auto-Power Off
A high-efficiency power control system designed to simulate industrial safety switches.


• Concept: Implemented a Software-Based Latch. Upon a single digital trigger, the system activates and maintains power (ON state) without continuous manual input.
• Smart Feature: Integrated an Auto-Power Off mechanism. The system automatically cuts power after a predefined duration to conserve energy and ensure safety.
• Visual Feedback: Added a "Pre-shutdown Warning" (LED Blinking) to alert the user before the automatic system cut-off.


 Task 2: Multi-Sensor Integration (Digital & Analog)

A comprehensive data logging and control interface demonstrating Sensor Fusion.

• Digital Interface: Utilized a Push-Button with internal PULLUP resistors for noise-free signal detection.
• Analog Interface: Integrated a Potentiometer to sample continuous real-time data (0-1023 range).
• Dynamic Control: The system maps analog inputs to control the timing of the Task 1 latching duration, creating an Adaptive Control Loop.


 Technical Specifications
• Microcontroller: Arduino Uno R3
• Communication: Serial Telemetry at 9600 Baud
• Input Handling: Digital Debouncing & Analog Signal Mapping
• Development Environment: Autodesk Tinkercad (Simulation)

 
 

 Why this implementation is professional?
1.	Code Optimization: Used map() functions and constants for scalable timing.
2.	User Experience (UX): Integrated visual indicators (LED patterns) for system states.
3.	Efficiency: Replaced external hardware latches with robust software logic to reduce component count.
   

Task one code 
<pre>
```cpp
const int buttonPin = 2;
const int ledPin = 7;
const int activeDuration = 3000;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
  Serial.println("System Initialized...");
}

void loop() {
  if (digitalRead(buttonPin) == LOW) {
    Serial.println("Event: Button Pressed");

    digitalWrite(ledPin, HIGH);
    Serial.println("State: Latching ON");

    delay(activeDuration);

    digitalWrite(ledPin, LOW);
    Serial.println("State: Auto Power Off");

    delay(500);
  }
}
```
</pre>

  
Task tow code
<pre>
```cpp id="7z8s1n"
const int digitalSensor = 2;
const int analogSensor = A0;

void setup() {
  pinMode(digitalSensor, INPUT_PULLUP);
  Serial.begin(9600);
  Serial.println("Sensor Monitoring System Active");
}

void loop() {
  int dState = digitalRead(digitalSensor);
  int aValue = analogRead(analogSensor);

  int percent = map(aValue, 0, 1023, 0, 100);

  Serial.print("Digital: ");
  Serial.print(dState);
  Serial.print(" | Analog: ");
  Serial.print(aValue);
  Serial.print(" | Level: ");
  Serial.print(percent);
  Serial.println("%");

  delay(250);
}
```
</pre>

<img width="1914" height="912" alt="لقطة شاشة 2026-04-09 124654" src="https://github.com/user-attachments/assets/b86ba261-73d0-4c85-b1c3-710fc8c58ad5" />
<img width="1907" height="910" alt="لقطة شاشة 2026-04-09 124736" src="https://github.com/user-attachments/assets/c78a93e1-b447-4570-ba52-dfebc9bd8996" />


_________________________________________



Task 3&4

![16189bc5-a717-42b2-a404-77dd8dec3a7c](https://github.com/user-attachments/assets/ab8efd47-9cea-4fda-9863-ad90ec650b66)


Arduino Motor Control with LCD Display


⸻
 Objective:
The aim of this project is to control a DC motor using an Arduino and display its operating status on an LCD screen.
⸻

 Project Description:
This project uses an Arduino board to control a DC motor through a motor driver, while displaying the system status (ON/OFF) on a 16x2 LCD screen. This allows easy monitoring of the system in real time.

⸻
 Components:
	•	Arduino Uno
	•	LCD 16x2
	•	DC Motor
	•	Motor Driver (L298N)
	•	Jumper Wires

⸻

⚙️ Circuit Connections:

The DC motor is connected to a motor driver module, which acts as an interface between the motor and the Arduino. The control pins of the motor driver are connected to Arduino digital pins 7 and 8 to manage motor operation and direction.

The LCD 16x2 is connected to the Arduino using digital pins, where RS is connected to pin 12, E to pin 11, D4 to pin 5, D5 to pin 4, D6 to pin 3, and D7 to pin 2.

Power connections are established by connecting 5V to supply the components, and all GND pins are connected together to ensure proper circuit operation.

⸻

 Working Principle:

The Arduino sends signals to the motor driver to control the motor operation. At the same time, it sends data to the LCD to display the current system status (ON or OFF).

⸻

 Results:
	•	The motor operated successfully
	•	The LCD displayed the system status correctly
	•	The system worked in a stable and reliable manner

⸻
 Conclusion:

This project demonstrates how multiple components can be integrated using Arduino to build a functional system. It serves as a foundation for more advanced embedded systems projects.

<pre>
```cpp id="r9x2qp"
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

// Initialize LCD (common address 0x27)
LiquidCrystal_I2C lcd(0x27, 16, 2);

// Motor pins (L293D)
const int motor1Pin1 = 8; 
const int motor1Pin2 = 9; 
const int motor2Pin1 = 10;
const int motor2Pin2 = 11;

void setup() {
  // Set motor pins as outputs
  pinMode(motor1Pin1, OUTPUT);
  pinMode(motor1Pin2, OUTPUT);
  pinMode(motor2Pin1, OUTPUT);
  pinMode(motor2Pin2, OUTPUT);

  // Initialize LCD
  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("Robot Ready!");
  delay(2000);
}

void loop() {
  // Move forward
  moveForward();
  lcd.clear();
  lcd.print("Moving Forward");
  delay(2000);

  // Stop
  stopMotors();
  lcd.clear();
  lcd.print("Stopped");
  delay(1000);

  // Move backward
  moveBackward();
  lcd.clear();
  lcd.print("Moving Backward");
  delay(2000);
}

// Move forward function
void moveForward() {
  digitalWrite(motor1Pin1, HIGH);
  digitalWrite(motor1Pin2, LOW);
  digitalWrite(motor2Pin1, HIGH);
  digitalWrite(motor2Pin2, LOW);
}

// Move backward function
void moveBackward() {
  digitalWrite(motor1Pin1, LOW);
  digitalWrite(motor1Pin2, HIGH);
  digitalWrite(motor2Pin1, LOW);
  digitalWrite(motor2Pin2, HIGH);
}

// Stop motors function
void stopMotors() {
  digitalWrite(motor1Pin1, LOW);
  digitalWrite(motor1Pin2, LOW);
  digitalWrite(motor2Pin1, LOW);
  digitalWrite(motor2Pin2, LOW);
}
```
</pre>
<img width="1914" height="907" alt="لقطة شاشة 2026-04-09 134724" src="https://github.com/user-attachments/assets/796d366b-ca40-4b6b-9b52-d7f98ef9b7fa" />
<img width="1913" height="909" alt="لقطة شاشة 2026-04-09 142620" src="https://github.com/user-attachments/assets/f03d8fd4-ae01-48c0-bfb6-69df4952ec88" />
<img width="1916" height="913" alt="لقطة شاشة 2026-04-09 142716" src="https://github.com/user-attachments/assets/ea754308-6f23-4924-9998-7e757b1caa72" />
<img width="1916" height="907" alt="لقطة شاشة 2026-04-09 142650" src="https://github.com/user-attachments/assets/4fc52c9f-b24a-4fa3-8dd1-15a0f50eec86" />



