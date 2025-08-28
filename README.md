## 🔄 Project Flowchart

```mermaid
flowchart TD

    Start([Start])
    Init[Initialize Peripherals\n(LCD, RTC, Keypad, ADC)]
    CheckTime[Read Current Time from RTC]
    MatchEvent{Does current time\nmatch any event?}
    Display[Fetch Event Message\nfrom memory]
    Scroll[Scroll message smoothly\non LCD]
    NoEvent[Wait/Idle\n(Keep checking time)]
    End([System Runs Continuously])

    Start --> Init --> CheckTime
    CheckTime --> MatchEvent
    MatchEvent -- Yes --> Display --> Scroll --> CheckTime
    MatchEvent -- No --> NoEvent --> CheckTime
