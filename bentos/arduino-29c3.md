---
layout: bento
title: Arduino@29C3
---

# Programming Arduino Workshop @ 29C3

![42]({{ site.baseurl }}bentos/arduino/42.jpg)

## Agenda

- Getting Started: Introduction to Arduino + Arduino Software
- The 12 LED-Shields
- Programming Exercise: Dice Library

# Getting Started

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

## Exercise
- Connect a LED to an arbitrary pin (using a 330 ohm Resitor) and let it blink. The cathode (usually the shorter lead) has to be connected to the negative voltage supply, on the arduino usually to ground (GND) - you can of course connect it the other way around, the Anode to 5V and the cathode to one of the output pins which has then to be set to "LOW" to let the led shine.

- (If you don't have an extra LED, you can also use the led on the board connected to pin 13 as in Examples->01.Basic->Blink., but actually connecting a LED by hand might give you a little impression how much fun tinkering with the arduino is!)

- if bored, you can connect the LED to one of the PWM pins (marked with ~, pins 3,5,6, 9, 10, 11) and let it fade, as shown in example 03.Analog->Fading.

![one led on arduino]({{ site.baseurl }}bentos/arduino/oneled.jpg)


# 12-LED-Shields

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

# Programming Exercise: Dice Library

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

# Events

* [Dec 28th 2012 1400 WS Hall 14 29c3](https://events.ccc.de/congress/2012/wiki/Arduino_*Programming*_Intro_%28for_other_genders%29)
