## 🔄 Project Flowchart

```mermaid
flowchart TD

    Start([Start])
    Init[Initialize Peripherals (LCD, RTC, Keypad, ADC)]
    CheckTime[Read Current Time from RTC]
    MatchEvent{Does current time match any event?}
    Display[Fetch Event Message from memory]
    Scroll[Scroll message smoothly on LCD]
    NoEvent[Wait/Idle - Keep checking time]
    End([System Runs Continuously])

    Start --> Init --> CheckTime
    CheckTime --> MatchEvent
    MatchEvent -- Yes --> Display --> Scroll --> CheckTime
    MatchEvent -- No --> NoEvent --> CheckTime
