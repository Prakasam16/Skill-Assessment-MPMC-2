# Generate 10 ms Delay Using Timer 1 (Mode 1) and Toggle LED on Port 1.0

## AIM
To write and execute an Assembly Language Program in the 8051 microcontroller to generate a 10 ms delay using Timer 1 in Mode 1 and toggle an LED connected to Port 1.0 continuously.

---

## APPARATUS REQUIRED
- 8051 Microcontroller Kit or Keil µVision Software
- LED and connecting wires
- Logic Analyzer or Oscilloscope (for timing verification)

---

## ALGORITHM
1. Start the program
2. Configure Port 1 as output for LED
3. Set Timer1 in Mode1 (16-bit) → `TMOD = 10H`
4. Load TH1 and TL1 to generate 10 ms delay
5. Start Timer (TR1 = 1)
6. Wait till Overflow Flag TF1 = 1
7. Stop Timer & Clear TF1
8. Toggle LED at P1.0
9. Repeat forever

---

## FLOWCHART
    ┌────────────────────────┐
    │        Start           │
    └──────────┬─────────────┘
               │
               ▼
    ┌────────────────────────┐
    │ Set Port 1 as Output   │
    │ TMOD = 10H             │
    └──────────┬─────────────┘
               │
               ▼
    ┌────────────────────────┐
    │ Load TH1, TL1 for 10ms │
    │ Start Timer (TR1=1)    │
    └──────────┬─────────────┘
               │
               ▼
    ┌────────────────────────┐
    │ Wait for TF1 = 1       │
    └──────────┬─────────────┘
               │
               ▼
    ┌────────────────────────┐
    │ Stop Timer             │
    │ Clear TF1              │
    │ Toggle LED (P1.0)      │
    └──────────┬─────────────┘
               │
               ▼
    ┌────────────────────────┐
    │   Repeat Forever       │
    └────────────────────────┘

---

## PROGRAM (Assembly - 8051)

```asm
; File: toggle_led_10ms_timer1.asm

ORG 0000H

MAIN:
    MOV P1, #00H        ; Set Port 1 as output
    MOV TMOD, #10H      ; Timer 1, Mode 1 (16-bit)

LOOP:
    SETB P1.0           ; Turn ON LED
    ACALL DELAY         ; Delay 10 ms

    CLR P1.0            ; Turn OFF LED
    ACALL DELAY         ; Delay 10 ms
    SJMP LOOP           ; Repeat forever

DELAY:
    MOV TH1, #0F2H      ; Load high byte for 10 ms delay
    MOV TL1, #04H       ; Load low byte for 10 ms delay
    SETB TR1            ; Start Timer 1

WAIT:
    JNB TF1, WAIT       ; Wait for overflow
    CLR TR1             ; Stop Timer
    CLR TF1             ; Clear overflow flag
    RET                 ; Return

END
```
## OUTPUT


## RESULT
The Assembly Language Program for the 8051 microcontroller was successfully written, assembled, and executed to generate a **10 ms delay using Timer 1 in Mode 1** and toggle an LED on **Port 1.0 continuously**.
