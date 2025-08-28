# RTC Based Event Board

## 1. Introduction
The **RTC Based Event Board** is a microcontroller-based real-time event display system built around the **LPC2148 ARM7 MCU**.  
It shows **scheduled messages**, **current time/date**, **day of the week**, and **temperature** on a 16x2 LCD.  

An administrator can update schedules, time, and date, or enable/disable messages using a **keypad-based password-protected menu**.  

---

## 2. Key Features
- ⏰ **Real-Time Clock (RTC):** Displays current time and date using LPC2148’s inbuilt RTC.  
- 📝 **Scheduled Messages:** Scrolls user-defined messages at preset times.  
- 🌡️ **Temperature Display:** Uses an **LM35 sensor** with ADC for real-time temperature monitoring.  
- 🔐 **Admin Settings:** Password-protected menu for editing time, date, day, and scheduled messages.  
- 🎛️ **User Interface:**  
  - **4x4 Keypad** for input.  
  - **16x2 LCD** for output.  
- ⚡ **Interrupt Support:** External interrupt (EINT0) provides quick access to admin settings.  
- 💡 **Status Indication:**  
  - **Green LED** – normal display mode.  
  - **Red LED** – message display mode.  

---

## 3. System Architecture  

### 🔧 Hardware Blocks
- **LPC2148 Microcontroller** – Core controller, manages logic and peripherals.  
- **16x2 LCD** – Displays time/date, temperature, and messages.  
- **4x4 Keypad** – User input for admin control.  
- **LM35 Temperature Sensor** – Feeds analog temperature to MCU ADC.  
- **RTC (built-in)** – Maintains accurate time and date.  
- **Status LEDs** – Indicate operating state.  

### 💻 Software Modules
- `Event_Board_Main.c` – System initialization, main loop, message scheduling.  
- `lcd.c/h` – LCD driver functions.  
- `kpm.c/h` – Keypad driver functions.  
- `rtc.c/h` – RTC setup and time/date management.  
- `adc.c/h` – ADC interface for temperature reading.  
- `settings.c/h` – Admin menu, password authentication, editing features.  
- `delay.c/h` – Delay utilities.  
- `pin_connect_block.c/h` – Pin configuration (PINSEL setup).  
- `types.h` – Custom data types for portability.  
- `defines.h` – Project-wide macros.  
- `Startup.s` – MCU startup/initialization file.  

---

## 4. Typical Operation
1. On boot, all peripherals initialize and RTC sets default time/date (if not already configured).  
2. **Main loop**:  
   - Reads RTC time continuously.  
   - Displays date, time, day, and temperature on LCD.  
   - At scheduled times → scrolls messages and switches LED to message mode.  
3. User can press the **EINT0 button** → enter admin menu.  
   - Enter correct password.  
   - Modify time/date/day/message settings.  
   - Enable or disable specific messages.  

---

## 5. File Structure
```plaintext
├── Event_Board_Main.c      # Main application logic
├── adc.c / adc.h           # ADC + LM35 interface
├── delay.c / delay.h       # Delay routines
├── lcd.c / lcd.h           # LCD driver
├── kpm.c / kpm.h           # Keypad driver
├── rtc.c / rtc.h           # RTC driver
├── settings.c / settings.h # Admin menu + password check
├── pin_connect_block.c/h   # Pin setup (PINSEL)
├── types.h                 # Custom typedefs
├── defines.h               # Macros and constants
├── Startup.s               # Startup code
├── *.d                     # Build dependencies
├── *.htm                   # Build logs/reports

---
6. How to Use
===========================

- Compile the project and flash it to the LPC2148.
- Connect hardware (LCD, keypad, LM35, LEDs) as per schematic.
- System will display time, date, day, and temperature by default.
- At scheduled times → messages scroll across LCD.
- Press EINT0 → enter admin mode.
- Input password.
- Modify settings (time/date/day/messages).
- Update admin password inside settings.c.


===========================
 7. Customization & Extensions
===========================

✏️  Modify scheduled messages in Event_Board_Main.c
🔑  Change admin password in settings.c
🔔  Add buzzer alerts or additional sensors
📺  Expand to 20x4 LCD for longer messages
🔌  Implement UART communication for PC logging
