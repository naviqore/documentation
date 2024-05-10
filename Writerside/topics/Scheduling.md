# Scheduling

Start typing here...

[Link to time schedule](https://docs.google.com/spreadsheets/d/1NVJV-sXO0yzrbKqA5deLzzR0VaGW3y-0jaoxKCRQ4sk/edit?usp=sharing)

| Person  | KW10 | KW11 | KW12 | KW13 | KW14 | KW15 | KW16 | KW17 | KW18 | KW19 | KW20 | KW21 | KW22 | KW23 | KW24 | KW25 | KW26 | KW27 | KW28 | KW29 | KW30 | KW31 | KW32 | KW33 | KW34 | KW35 | KW36 | Total |
|---------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|-------|
| Merlin  |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      | 375h  |
| Lukas   |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      | 375h  |
| Michael |      |      |      | V🌴  | 8h   | 4h   | 9h   | 8h   | 2h   | 20h  | 12h  | 13h  |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      | 375h  |

## Legend

| Symbol | Meaning                             |
|--------|-------------------------------------|
| KW     | Calendar Week                       |
| V🌴    | Vacation                            |
| Total  | Sum of time estimates for all weeks |

```mermaid
gantt
    dateFormat YYYY-MM-DD
    title Arbeitsstundenplan

    section Merlin
        März: a1, 2022-03-01, 31d
        April: a2, after a1, 30d
        Mai: after a2, 31d
        Juni: after a1, 30d
        Juli: after a1, 31d
        August: after a1, 31d
        September: after a1, 30d
        Total: crit, 2022-03-01, 204d

    section Lukas
        März: b1, 2022-03-01, 31d
        April: after b1, 30d
        Mai: after b1, 31d
        Juni: after b1, 30d
        Juli: after b1, 31d
        August: after b1, 31d
        September: after b1, 30d
        Total: crit, 2022-03-01, 204d

    section Michael
        März: c1, 2022-03-01, 31d
        April: after c1, 30d
        Mai: after c1, 31d
        Juni: after c1, 30d
        Juli: after c1, 31d
        August: after c1, 31d
        September: after c1, 30d
        Total: crit, 2022-03-01, 204d
```

```mermaid
timeline
    title MermaidChart 2023 Timeline
    section 2024 MARCH <br> Analysis
        Merlin: KW11 (8h): KW12 (8h)
                : KW13 (8h)
        Lukas: KW11 (8h): KW12 (8h)
                : KW13 (8h)
        Michael: KW11 (8h): KW12 (8h)
                : KW13 (8h)
    section 2024 APRIL <br> Analysis
        Merlin: KW11 (8h): KW12 (8h)
                : KW13 (8h)
        Lukas: KW11 (8h): KW12 (8h)
                : KW13 (8h)
        Michael: KW11 (8h): KW12 (8h)
                : KW13 (8h)

```
