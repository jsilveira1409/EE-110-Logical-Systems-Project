# Logicwatch

Course: EPFL - EE110 - Logic systems (autumn semester 2017/2018)

Project: a digital multifunction watch implemented using only logic gates ⌚

## Physical constraints

- Two push buttons A and B
- Six seven-segment displays (SSDs)
- Ten LEDs
- One power-on-reset button
- One clock (2KHz crystal oscillator)

The project is meant to run on a Terasic DE10-Lite FPGA board. Since it is a real physical system, non-ideal effects have been taken into account (buttons bouncing, non-perfect simultaneous press of buttons, undefined initial state of the system, etc).

## Features

The watch has five distinct operation modes (time, stopwatch, alarm, time setting, countdown). Pressing A and B simultaneously for a longer period of time allows to change the active mode in a circular manner (1 -> 2 -> 3 -> 4 -> 5 -> 1 -> 2 -> etc). The first five LEDs (n°0-4) indicate which mode is currently active.

### Mode 1 - Time

Time is kept with the format {month - day of the week - date - hours - minutes - seconds}. Pressing on A allows to change from the display of {month - day of the week - date} to {hours - minutes - seconds} and vice-versa. Pressing on B changes the time format from european to american and vice-versa. When using the american time format, LEDs n°6-7 indicate whether time is AM (n°6) or PM (n°7).

### Mode 2 - Alarm

The first four SSDs from the left indicate {hour - minute} at which the alarm should sound. The sixth SSD (far right) is either one (alarm ON) or zero (alarm OFF). At any time and on any mode, the tenth LED (far right) indicates whether the alarm is On or OFF. 

The SSD of the field being modified blinks. Pressing button A increments the field being modified. Pressing B changes the field being modified (from left to right).

When the alarm "sounds", a special LED animation is triggered. To stop it, any button can be pressed.

### Mode 3 - Stopwatch

Stopwatch indicates {minutes - seconds - centiseconds}. Pressing on B resume/pause the chronometer. Pressing on A while the chronometer is paused will reset it at zero. Pressing A while the chronometer is running will do nothing.

### Mode 4 - Time setting

Similarly to alarm setting, the SSD of the field being modified blinks. Pressing A increments the field being modified. Pressing B changes the field being modified (from left to right). After going through every field with B (month -> day -> date -> hour -> minute -> second) none of the SSDs blink. At this point pressing A will validate the changes, while pressing B will bring the user back to modifying the month and then all the other fields.

### Mode 5 - Countdown

It is possible to set a countdown with {hours - minutes - seconds}. The setting of start time is similar to previous modes. Current field being modified is blinking. Pressing A increments the value. Pressing B changes the field being modified. When no SSD blinks anymore, pressing A will start the countdown while pressing B will return to setting the start time.

When the countdown is running, pressing A will pause/resume it. When the countdown is paused, pressing B will allow to set the start time as previously described.

### Power-on-reset (PoR)

Pressing the PoR button will reset every mode with its default values. It is important as it allow to put the system in a known state and thus guarantee a correct behaviour.

## Notable technical solutions

- Various finite state machines
- React to falling-edge only systems
- Switch debouncing system
- Simultaneous button press detector
- PoR initialization
- (...)

## How to use it

Launch `logisim-evolution-2.13.19.jar` and from there open `MAIN.circ`. Then you can start the simulation. Depending on your computer performance and the settings of the simulation, time will most likely not be accurate. It can however be calibrated by modifying certain logic circuits.
