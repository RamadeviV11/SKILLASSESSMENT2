# SA2 MPMC RAMADEVI_V
# 500µS DELAY USING TIMER 0 IN MODE 2 AND TOGGLE PORT 1.3
## AIM
To generate a 500 µs delay using Timer 0 in Mode 2 of the 8051 microcontroller and toggle Port 1.3, and to verify the output waveform using KEIL µVision Logic Analyzer.

---

## APPARATUS REQUIRED
- Personal computer with KEIL Software

---

## ALGORITHM

1.Configure Timer 0 in Mode 2 (8-bit auto-reload mode).

2.Load TH0 and TL0 with the appropriate value to generate 500 µs delay.

3.Start Timer 0.

4.Continuously poll the Timer 0 overflow flag (TF0).

5.On Timer overflow, stop Timer 0, clear the overflow flag.

6.Toggle bit 3 of Port 1 (P1.3).

7.Reload the timer and restart Timer 0.

8.Repeat to generate continuous toggling with 500 µs delay.

---

## FLOWCHART
<img width="2048" height="2048" alt="image" src="https://github.com/user-attachments/assets/bef14f16-d6c0-4dee-a95e-5618c42eb67e" />


---

## PROGRAM
```asm
ORG 0000H
MAIN:
    MOV TMOD, #02H       ; Timer0 in Mode 2 (8-bit auto reload)
    MOV TH0, #0CH        ; Load TH0 with 0CH for ~244 µs delay
    SETB TR0             ; Start Timer0
AGAIN:
    ACALL DELAY_500US    ; Call 500 µs delay
    CPL P1.3             ; Toggle Port 1.3
    SJMP AGAIN           ; Repeat forever
DELAY_500US:
    MOV R2, #2           ; 2 overflows ˜ 488 µs
WAIT1:
    JNB TF0, WAIT1       ; Wait till timer overflows
    CLR TF0              ; Clear overflow flag
    DJNZ R2, WAIT1       ; Repeat for 2 overflows
    RET
END

```
## OUTPUT
![OUTPUT](https://github.com/user-attachments/assets/65e4059a-be89-4501-b256-73c8fee0cea1)


---


## RESULT

The program was successfully executed in KEIL. Using the internal Logic Analyzer, the toggle wave output on P1.3 with delay of approximately 500 µs was verified, indicating correct timer configuration and program flow.

---
