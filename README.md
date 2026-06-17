# PIC18F4550 7-Segment Counter Using Lookup Table

Assembly project for the PIC18F4550 microcontroller that implements a button-controlled hexadecimal counter displayed on a 7-segment display. The program uses a lookup table with `RETLW` instructions to translate counter values into 7-segment display codes.

This project was developed as an embedded systems practice to reinforce low-level programming, digital input/output control, lookup tables, macros, and register-level operations in PIC Assembly.

## Features

* Reads a push button input from PORTB.
* Increments a counter each time the button is pressed.
* Counts from `0` to `31`.
* Displays values using a 7-segment display connected to PORTD.
* Uses a lookup table with `RETLW` instructions for display decoding.
* Supports hexadecimal digits from `0` to `F`.
* Includes additional display codes with decimal point enabled.
* Implements a software delay routine for button timing/debouncing.

## Technologies Used

* PIC18F4550 microcontroller
* Assembly language
* MPLAB / MPASM
* Digital I/O ports
* 7-segment display
* Lookup table with `RETLW`
* Software delay routines

## Project Structure

```text
src/
├── seven_segment_counter.asm   # Main Assembly source file
├── config.h                    # PIC18F4550 configuration bits
└── Disp7seg.h                  # 7-segment display codes
```

## How It Works

1. PORTB is configured as input.
2. PORTD is configured as output.
3. The counter variable is initialized to zero.
4. The program waits for a button press on PORTB bit 7.
5. When the button is pressed, the counter increments.
6. If the counter reaches `32`, it resets to `0`.
7. The counter value is sent to a lookup table.
8. The lookup table returns the corresponding 7-segment display code.
9. The display is updated through PORTD/LATD.

## Lookup Table

The project uses a lookup table implemented with `RETLW` instructions. The counter value is multiplied by two to calculate the correct program memory offset, since each table entry occupies two instruction bytes.

```asm
TABLE7
    MULLW 2
    MOVF PRODL, aw
    ADDWF PCL, af
    RETLW disp0
    RETLW disp1
    RETLW disp2
    ...
    RETLW dispF
```

This technique allows the program to efficiently map numerical values to display patterns without using long chains of comparisons.

## Learning Outcomes

Through this project, I practiced:

* Programming a PIC18F4550 microcontroller in Assembly.
* Configuring digital input and output ports.
* Using macros to simplify repetitive display operations.
* Implementing lookup tables with `RETLW`.
* Working with program counter manipulation using `PCL`.
* Handling button input in low-level embedded systems.
* Creating software-based delay routines.
* Displaying hexadecimal values on a 7-segment display.

## Notes

This project was originally developed as an academic embedded systems practice and later organized as part of a technical portfolio.
