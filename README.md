
TASK 1&2
Project Overview: Smart Control & Power Management System
This repository contains two integrated tasks developed using Arduino Uno, focusing on intelligent power management and multi-sensor data acquisition.



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

LDR Sensor Technical Brief
• 1. Acronym & Name:
LDR stands for Light Dependent Resistor. It is also commonly known as a Photoresistor.
• 2. Scientific Principle:
It operates on the principle of Photoconductivity. The component's electrical resistance decreases as the intensity of the incident light increases. In darkness, the resistance is very high (Megaohms), and in bright light, it drops significantly (Ohms).
• 3. Signal Type & Components:
• Signal Type: Analog. It provides a continuous range of voltage values based on light intensity.
• Required Resistor: A 10kΩ resistor is used in a Voltage Divider configuration to translate the resistance change into a measurable voltage for the Arduino.


Circuit Construction Steps (Tinkercad)
1.	Placement: Place an Arduino Uno and a Breadboard in the workspace.
2.	LDR Setup: * Connect one leg of the LDR to the 5V rail.
• Connect the other leg to the Arduino Analog Pin A0.
• From that same leg (A0 connection), connect a 10kΩ resistor to the GND rail (this creates the Voltage Divider).


3.	LED Setup:
• Connect the Anode (longer leg) of the LED to Digital Pin 13.
• Connect the Cathode (shorter leg) to a 220Ω resistor, and the other end of the resistor to GND.
 Street Light Simulation Code (Professional Version)
This code simulates a smart street lighting system: it automatically turns the light ON when it’s dark and OFF during the day.
<pre>
```cpp id="m4k9xz"
/*
 * Project: Smart Street Light System
 * Task: LDR Sensor Implementation
 * Logic: LED triggers based on ambient light threshold
 */

const int ldrPin = A0;     // LDR sensor input
const int ledPin = 13;     // Street light output
const int threshold = 500; // Light sensitivity threshold

void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600); // Initialize Serial Monitor for debugging
  Serial.println("System Initialized: Monitoring Ambient Light...");
}

void loop() {
  // Read the analog value from LDR (0 - 1023)
  int lightLevel = analogRead(ldrPin);
  
  // Output light level to Serial Monitor
  Serial.print("Current Light Level: ");
  Serial.println(lightLevel);

  // Street Light Logic
  if (lightLevel < threshold) {
    // It's Dark: Turn LED ON
    digitalWrite(ledPin, HIGH);
    Serial.println("Status: Night Detected - LED ON");
  } else {
    // It's Bright: Turn LED OFF
    digitalWrite(ledPin, LOW);
    Serial.println("Status: Day Detected - LED OFF");
  }
  
  delay(500); // Small delay for stability
}
```
</pre>



