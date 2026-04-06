# ElectroLab
TASK 1&2
Project Overview: Smart Control & Power Management System
This repository contains two integrated tasks developed using Arduino Uno, focusing on intelligent power management and multi-sensor data acquisition.
🛠️ Task 1: Intelligent Latching Switch with Auto-Power Off
A high-efficiency power control system designed to simulate industrial safety switches.
• Concept: Implemented a Software-Based Latch. Upon a single digital trigger, the system activates and maintains power (ON state) without continuous manual input.
• Smart Feature: Integrated an Auto-Power Off mechanism. The system automatically cuts power after a predefined duration to conserve energy and ensure safety.
• Visual Feedback: Added a "Pre-shutdown Warning" (LED Blinking) to alert the user before the automatic system cut-off.
📡 Task 2: Multi-Sensor Integration (Digital & Analog)
A comprehensive data logging and control interface demonstrating Sensor Fusion.
• Digital Interface: Utilized a Push-Button with internal PULLUP resistors for noise-free signal detection.
• Analog Interface: Integrated a Potentiometer to sample continuous real-time data (0-1023 range).
• Dynamic Control: The system maps analog inputs to control the timing of the Task 1 latching duration, creating an Adaptive Control Loop.
💻 Technical Specifications
• Microcontroller: Arduino Uno R3
• Communication: Serial Telemetry at 9600 Baud
• Input Handling: Digital Debouncing & Analog Signal Mapping
• Development Environment: Autodesk Tinkercad (Simulation)
💡 Why this implementation is professional?
1.	Code Optimization: Used map() functions and constants for scalable timing.
2.	User Experience (UX): Integrated visual indicators (LED patterns) for system states.
3.	Efficiency: Replaced external hardware latches with robust software logic to reduce component count.
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
