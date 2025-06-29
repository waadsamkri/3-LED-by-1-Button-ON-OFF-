# 3-LED-by-1-Button-ON-OFF-
Arduino 3-LED by 1 Button( ON/OFF)


This Arduino project demonstrates how to control multiple LEDs using a single push-button. Each press of the button toggles the LEDs ON or OFF simultaneously.

## 🛠️ Features

- Controls **3 LEDs** (connected to pins 13, 12, and 11)
- Uses **1 button** (connected to pin 2)
- **Toggles all LEDs ON or OFF** with each button press
- Built-in **debounce** logic to prevent false triggers

## 📷 Hardware Setup

### 🧩 Components Required
- 1 x Arduino board (Uno, Nano, etc.)
- 3 x LEDs
- 3 x 220Ω resistors
- 1 x Push-button
- Jumper wires
- Breadboard

### 🔌 Pin Connections

| Component | Arduino Pin | Notes                       |
|----------|-------------|-----------------------------|
| LED 1     | 13          | Connect through a resistor to GND |
| LED 2     | 12          | Connect through a resistor to GND |
| LED 3     | 11          | Connect through a resistor to GND |
| Button    | 2           | Connect between pin and GND        |

> The button uses `INPUT_PULLUP`, so no external pull-up resistor is needed.

## 🔁 How It Works

- On startup, all LEDs are OFF.
- When the button is **pressed**, the program detects a transition from **HIGH to LOW**.
- It toggles the state of the `ledState` boolean.
- All three LEDs are then set to the new state (ON or OFF).
- A `delay(200)` is used for simple **debouncing**.

## 💻 Code Snippet

```cpp
#define LED_1_PIN 13
#define LED_2_PIN 12
#define LED_3_PIN 11
#define BUTTON_PIN 2

bool ledState = false;
bool lastButtonState = HIGH;
bool currentButtonState;

void setup() {
  pinMode(LED_1_PIN, OUTPUT);
  pinMode(LED_2_PIN, OUTPUT);
  pinMode(LED_3_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT_PULLUP);
}

void loop() {
  currentButtonState = digitalRead(BUTTON_PIN);

  if (lastButtonState == HIGH && currentButtonState == LOW) {
    ledState = !ledState;
    updateLEDs(ledState);
    delay(200);
  }

  lastButtonState = currentButtonState;
}

void updateLEDs(bool state) {
  digitalWrite(LED_1_PIN, state ? HIGH : LOW);
  digitalWrite(LED_2_PIN, state ? HIGH : LOW);
  digitalWrite(LED_3_PIN, state ? HIGH : LOW);
}
