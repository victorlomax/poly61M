# Syncing the Korg Poly 61M arpeggiator to MIDI Clock

This project intend to sync the Poly61M arpeggiator to MIDI Clock. When a MIDI Clock pulse will be received:
- the internal clock will be disabled
- pulses are sent to the arpeggiator

STEP CONTROL
==================================
The Arpeggiator Speed potentiometer allows to control the steps of the arpeggiator, 
i.e. the number of MIDI clock events per pulse.
The MIDI Clock is presumed to be 24 ppqn (pulse per quarter note).
Position of the potentiometer 
- 0 (fully CCW) = 1/4: a pulse is sent every 96 MIDI Clock message received
- ~ 1.5 = 1/3: a pulse is sent every 72 MIDI Clock message received
- ~ 3 = 1/2: a pulse is sent every 48 MIDI Clock message received
- 5 = 1: a pulse is sent every 24 MIDI Clock message received
- ~ 7 = 2: a pulse is sent every 12 MIDI Clock message received
- ~ 8.5 = 3: a pulse is sent every 8 MIDI Clock message received
- 10 (fully CW) = 4: a pulse is sent every 6 MIDI Clock message received

CLOCK PATTERN
==================================
Up the 16 clock patterns can be set (tbc)...

SYSEX
==================================
- F0 42 30 7F 00 00 F7 : Fully manual mode. User must press the Arpeggiator button to start the arpeggiator. 
- F0 42 30 7F 00 01 F7 : The arpeggiator starts and stops on received MIDI Start (0xFA) and Stop (0xFC) events.
- F0 42 30 7F 00 02 F7 : The arpeggiator automatically starts on first MIDI clock (0xF8) and stops after 4 missing clock.
- F0 42 30 7F 01 00 F7 : Select clock pattern 0
- ...
- F0 42 30 7F 01 0F F7 : Select clock pattern 15
- F0 42 30 7F 10 -- -- -- F7 : Set clock pattern 0
- ...
- F0 42 30 7F 1F -- -- -- F7 : Set clock pattern 15

LINKS
==================================
- 8049 Spy, how to dump a 8048/8049: https://www.sbprojects.net/projects/8049spy/index.php
- A low cost MIDI interface for Korg Poly61: http://www.tauntek.com/Poly61.htm
- Bit banging MIDI on ATTiny: https://mitxela.com/projects/midi_on_the_attiny
