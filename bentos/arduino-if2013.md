---
layout: bento
title: Arduino
---

# Programming Arduino Workshop @ Informatica Feminale 2013

![42]({{ site.baseurl }}bentos/arduino/42.jpg)

## Table of Contents
* This will become a table of contents (this text will be scraped).
{:toc}

## Important Links
* [Informatica Feminale 2013](http://www.informatica-feminale.de)
* [Informatica-Programm](http://www.informatica-feminale.de/Sommer2013/lib/ajax/course.php?courseId=503)
* [Arduino](http://arduino.cc)
* [C++ Reference](http://www.cplusplus.com/reference/)
* [C++ Tutorial](http://www.cplusplus.com/doc/tutorial/)
## Agenda & Tentative Schedule


| Time |             |      | Content  |
|:-----|:------------|-----:|:---------|
| Mi   | 11.00-12.30 | 1.5  | Getting Started: Installation and first   blinking LED ||
| Do   | 09.00-12.30 | 3 | 12-LED Shields and Dice Library |
| Do   | 14.00-15.30 | 1.5| Dice Library Extensions|
| Fr   | 09.00-12.30 | 3 | TBD |
| Fr   | 14.00-15.30 | 1.5 | TBD |

# Getting Started: Installation and first blinking LED

Please prepare this before coming to Informatica Feminale!
We will use the first (short!) session on Wednesday to clarify questions with it, connect the Arduino and let the LED blink.

Arduino is a hardware prototyping platform based on Atmel Atmega Microprocessors, in case of the Arduino Uno which we will be using in the workshop the Atmel Atmega 328. Probably the best thing about Arduino is
the vast amount of documentation and project examples you can find on the net, which is why I will not try to replicate any of that here and dive right into a short step-by-step guide to getting started programming it.

- Download the Arduino Software (IDE) for your Platform: [Arduino Software](http://arduino.cc/en/Main/Software)
- Have a look at some examples (In the Arduino Software: File->Examples), especially

  - 01\.Basics->Blink,
  - 02\.Digital->BlinkWithoutDelay and
  - 02\.Digital->Button,

  which will be helpful for the exercises below, but feel free to have a look at all the other examples! These are "Arduino Sketches", which contain two methods: setup and loop. You put all setup code (e.g. initializing pins as input or output pins, seeding the random function) in setup and everything else in loop which will be called repeatedly. You can define variables outside the methods as shown in the BlinkWithoutDelay example.

- The Programming Language is a subset of C++ ([ARV-Toolchain](http://nongnu.org/avr-libc/user-manual/)). Basic control structures are shown in various examples in 05.Control. The Arduino software comes with a library on top of AVR that has a lot of nice functions:
- Have a look at the Arduino Library: [Arduino Language Reference](http://arduino.cc/en/Reference/HomePage)

- Debugging: You can use the Serial communication to print out debugging messages from your sketch. See 04.Communication->ASCIITable for an example.

- All Examples are also [documented on the arduino page](http://arduino.cc/en/Tutorial/HomePage) including the circuits needed for running them.

## LED-Exercise
- Connect a LED to an arbitrary pin (using a 330 ohm Resitor) and let it blink. The cathode (usually the shorter lead) has to be connected to the negative voltage supply, on the arduino usually to ground (GND) - you can of course connect it the other way around, the Anode to 5V and the cathode to one of the output pins which has then to be set to "LOW" to let the led shine.

- (If you don't have an extra LED, you can also use the led on the board connected to pin 13 as in Examples->01.Basic->Blink., but actually connecting a LED by hand might give you a little impression how much fun tinkering with the arduino is!)

- if bored, you can connect the LED to one of the PWM pins (marked with ~, pins 3,5,6, 9, 10, 11) and let it fade, as shown in example 03.Analog->Fading.

![one led on arduino]({{ site.baseurl }}bentos/arduino/oneled.jpg)

# Introduction: 12-LED-Shields

I've prepared simple leds shields to get you started with a bit of Arduino-Programming without
the need to put together or solder own prototypes. The shields let you try out some first microcontroller programming with physical interaction with the real world: reading a button state and switching
leds on and off! (hey, it's not a computer display!)

![12 LED Shield]({{ site.baseurl }}bentos/arduino/led12-shield-foto.jpg)

The shields have 12 LEDs directly connected to 12 (output) pins, and one or two buttons connected to two other pins, as shown in the diagram below (for just four LEDs and 1 Button).

The Buttons feature a pull down resistor making sure that you read a proper "LOW" on the input pins while the button is not pressed. You can explore the button starting with the 02.Digital->Button Example.

![12 LED Shield]({{ site.baseurl }}bentos/arduino/led12-shield.jpg)

As most of the shields have been soldered a bit differently, I've provided a header file containing variables with the pin information: [pins.h](https://github.com/drblinken/arduino-workshop/blob/master/BoardTest/pins.h) which you can download and use in our own sketches.
To use them, you have to declare your board before including pins.h like this:

      #define BOARDn

where n is the number of your board, e.g. for B4 as in the picture above you would change the line to

      #define BOARD4

LEDs: use the int array  int pins\[\] which lists the pins from the lower right
corner to the upper left like this:

     11 10 09 08
     07 06 05 04
     03 02 01 00

e.g. to switch on the two middle leds, use:

     digitalWrite(pins[05],ON);
     digitalWrite(pins[06],ON);

(Note that I rather use ON and OFF than LOW and HIGH - one of the shields is connected the other way around, so this is abstracted as well ;-)

If you use pins.h, you can read the button state like this:

    buttonState1 = digitalRead(buttonPin1);
    buttonState2 = digitalRead(buttonPin2);

Have a look at the [BoardTest Sketch](https://github.com/drblinken/arduino-workshop/tree/master/BoardTest) in the arduino workshop example repository on
[GitHub](https://github.com/drblinken/arduino-workshop)

Note: some of the shields still have leds connected to pins 0 and 1 which are also used for serial communication. If you have trouble uploading sketches while animations are running, make sure to disconnect them (just don't push those two leads in when clipping the shield on) - they should be connected to two other pins as well.

# First Day: Dice Library Programming Exercise

Write a Sketch that implements a simple Die:
The Goal is to implement a simple six-sided Die that can be rolled by pressing a button.

To implement it, you will need the random() function provided by the Arduino library ([Reference](http://arduino.cc/en/Reference/HomePage)). It's also a good idea to write a function showing different numbers on the die, e.g.

    showNumber(int number)

You can use the Sketch [DiceLibrary](https://github.com/drblinken/arduino-workshop/tree/master/DiceLibrary) as a starting point. It features a header and a class file for the DiceLibrary class where you just have to fill out the methods:

    void roll(); // rolls the Die and displays result
    void showNumber(int number) // shows a number between 1 and 6

## Ideas for Extensions
- roll the die 2 times, showing the numbers in alteration and hiding them using the second button if available.
- show nice animations while the die is rolling.


# Second Day: Arduino BlinkenFilm or own Project

This is a suggestion for a project for the second day of our workshop. It can be done with the 12 LED-Shields, and features somewhat more complex programming.

This is only a suggestion, though - if you'd rather work on your own project, go ahead!

Check out project blinkenlights - <a href="http://blinkenlights.net/project"> http://blinkenlights.net/project </a> - at least watch the video <a href="http://blinkenlights.net/project/videos">http://blinkenlights.net/project/videos</a> to get an idea about what the project blinkenlights was and what you could have done with a BlinkenLightsMovie back in 2001.

This exercise is about playing blinkenlights movies in BLM format on the arduino and the 12led shield by sending a movie file to the Arduino which it then stores and plays in a loop. Reading a file in and switching the according LEDs on and off doesn't seem to be a big issue. But there are two mayor obstacles: First, the Arduino doesn't have a file system. Second, it has very restricted memory available, so we want to store the file in a very compressed format.

## Preparation

* Have a look at the Blinkenlights Movie&nbsp;Format: <br> [http://oldwiki.blinkenarea.org/bin/view/Blinkenarea/BlinkenLightsMovie](http://oldwiki.blinkenarea.org/bin/view/Blinkenarea/BlinkenLightsMovie)
* Update your Knowledge about Bitshift Operators. How can you pack two bytes into an two-byte integer? How four nibbles? How can you determine if the nth bit is set in an byte or integer? see <a href="http://arduino.cc/en/Reference/Bitshift">http://arduino.cc/en/Reference/Bitshift</a></li>
* If you haven't already done so for debugging the prior exercise, read about serial communication on the Arduino. <a href="http://arduino.cc/en/Reference/Serial">http://arduino.cc/en/Reference/Serial</a>
* Design a State Machine which parses an BLM file byte by byte: you will have an initial state switching to the "reading delay" state when an @ is read etc.


## Playing BLM files
For playing BLM files on the Arduino, we will first compress them and send the compressed version to the Arduino, to make the processing on the Arduino fast enough to not loose any sent data. This is a lot of work, so you might want to split up and have one person working on the Arduino part, and the other on the file compression. Check out the section about "BLM Compression" below.

You can use the [This Sketch](https://github.com/drblinken/arduino-blinkenfilm) as a starting point for your implementation.

### Part1: Show a frame.

Create a method showFrame(int frame){} in an Arduino Sketch  that interprets the passed integer as a movie frame in the described compression. Also provide helper methods to normalize and denormalize the delay in bits 16-13 (these are also provided with the scaffold). Test this method by implementing a binary count up to 4096 using the loop() function rather than a for loop to be able to check for incoming films later at every count step (that is, implement doCount() in the scaffold).

### Part2: Receive and store a received Blinkenfilm.
Receive a compressed film and store it in an byte/integer array or in EEPROM. Use Serial.read to receive films send via the Serial interface by receiving single bytes and storing them somewhere - every first byte represents the upper byte in the integer frame, every second the lower byte.
Test this by sending bytes manually using the Serial Console in the Arduino software. The Arduino has only 1k memory for variables, so you may want to use the EEPROM to store the film. This enables you to make the Serial Buffer large enough to handle even long films by editing HardwareSerial.cpp:


    #define SERIAL_BUFFER_SIZE 640

you'll find the file among the libraries installed with the arduino software, e.g. on the Mac here:

    /Applications/Arduino.app/Contents/Resources/Java/hardware/arduino/cores/arduino/HardwareSerial.cpp
On Linux and the Mac, you can send Bytes and Files to the arduino by using this:

    echo 'BARBARA' > /dev/tty.usbmodemfd121

or

    cat film.blm > /dev/tty.usbmodemfd121

On Windows, you can just copy & paste the compressed bytestring from the file into the serial monitor. Just make sure no formatting information is added - use a plain text editor and select "no line ending" in the monitor.

### Extra Part

C++ (or other language) Command Line Utility: BLM Compression: write a simple C++ command line utility that converts regular BLM files into the compressed format by simply chaining the bytes together. Use the state machine you've designed in the prelab and implement it with a simple switch statement. This is a brief program that could be done in C essentially - that is, don't bother about creating classes, just write one or two subroutines called by main that parse the file.


## BLM Compression
Here's a simple Idea on how the BLM could be compressed for the Arduino:
If you have a frame with a duration and three rows with 4 leds:

    @100
    1010
    1111
    0110

These can be compressed into two bytes (or one integer) by simply converting the rows into nibbles (4 bits) using the 12 rightmost bits:

    101011110110

Now, compressing the duration is a bit harder, and can't really be done with the remaining nibble, as it can only represent 16 different states. One way is to restrict the films to 50 ms duration steps up to 800 ms, which is actually quite sufficient. 100/50 = 2 = 0b0010, such that you get this altogether:

    0010101011110110
    dddd333322221111

You might, however, choose to compress BLM differently - this is just a suggestion!

# AVR-Programming with Eclipse
If you want "the real thing", you can also set up Eclipse for AVR-Programming, you find a manual <a href="http://arduino.cc/playground/Code/Eclipse">here</a>. You basically need the CDT (C development tools) for eclipse, the AVR Kit, the Arduino libraries and a lot of configuration, but it looks more complicated as it actually is. In any case, I recommend using the Arduino Software for browsing through the examples, and you'll need it for the libraries, so make sure to have that, too.
