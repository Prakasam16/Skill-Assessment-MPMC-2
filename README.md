Generate 10 ms Delay Using Timer 1 (Mode 1) and Toggle LED on Port 1.0
AIM

To write and execute an Assembly Language Program in the 8051 microcontroller to generate a 10 ms delay using Timer 1 in Mode 1 and toggle an LED connected to Port 1.0 continuously.

APPARATUS REQUIRED

8051 Microcontroller Kit or Keil µVision Software

LED and connecting wires

Logic Analyzer or Oscilloscope (for timing verification)

ALGORITHM

Start the program.

Configure Port 1 as output for connecting the LED.

Set Timer 1 in Mode 1 (16-bit timer mode) using TMOD = 10H.

Load TH1 and TL1 registers with values to generate 10 ms delay.

Start Timer 1 by setting TR1 = 1.

Wait until Timer Overflow Flag TF1 becomes 1.

Stop Timer and clear the overflow flag TF1.

Toggle the LED connected to Port 1.0.

Repeat the above steps continuously.

FLOWCHART
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

PROGRAM
ORG 0000H

MAIN:
    MOV P1, #00H        ; Configure Port 1 as output
    MOV TMOD, #10H      ; Timer 1 Mode 1 (16-bit)

LOOP:
    SETB P1.0           ; Turn ON LED
    ACALL DELAY         ; Call delay routine

    CLR P1.0            ; Turn OFF LED
    ACALL DELAY         ; Call delay routine
    SJMP LOOP           ; Repeat forever

DELAY:
    MOV TH1, #0F2H      ; Load high byte for 10 ms delay
    MOV TL1, #04H       ; Load low byte for 10 ms delay
    SETB TR1            ; Start Timer 1

WAIT:
    JNB TF1, WAIT       ; Wait for overflow flag
    CLR TR1             ; Stop Timer
    CLR TF1             ; Clear Timer flag
    RET                 ; Return

END

OUTPUT


RESULT

Thus, the Assembly Language Program for the 8051 microcontroller to generate a 10 ms delay using Timer 1 in Mode 1 and toggle an LED on Port 1.0 continuously was successfully written, assembled, and executed.
