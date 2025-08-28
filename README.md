## 🔄 Project Flowchart

```mermaid
flowchart TD

    Start([Start])
    Init[Initialize Peripherals <br> (LCD, RTC, Keypad, ADC)]
    CheckTime[Read Current Time <br> from RTC]
    MatchEvent{Does current time <br> match any event?}
    Display[Fetch Event Message <br> from memory]
    Scroll[Scroll message smoothly <br> on LCD]
    NoEvent[Wait/Idle <br> (Keep checking time)]
    End([System Runs Continuously])

    Start --> Init --> CheckTime
    CheckTime --> MatchEvent
    MatchEvent -- Yes --> Display --> Scroll --> CheckTime
    MatchEvent -- No --> NoEvent --> CheckTime
