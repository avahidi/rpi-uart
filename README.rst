
rpi-uart
========


This UART board for the Raspberry Pi, is one of those Sunday morning projects that turned out to be quite useful.
It lets you to power and talk to the board using only a micro-USB cable. Hence you can go from this mess


.. image:: doc/before.jpg
    :alt: connecting to the rpi using a serial to USB cable

. . . to this:


.. image:: doc/after.jpg
    :alt: connecting to the rpi using this board


To me the main advantage of this is that I can quickly move it between different boards.


Open hardware
-------------

The PCB was developed using KiCad and is published under the CERN Open Hardware License v1.2.

.. image:: doc/pcb.jpg

Some footprints have been modified to eliminate oval plated holes which may be expensive to manufacture.
I have also tried to make the design easy to solder, although you may still find the fine-pitch USB connector a bit challenging.
The CH340g IC was chosen to avoid depending on FTDI or counterfeit FTDI chips.

Operations modes
----------------

The board can be populated in a couple of ways to allow different powering modes.
Only one of which will not fry your Raspberry Pi so pay attention to this!

.. image:: doc/schematics.png


RPi mode
~~~~~~~~

To connect directly to a Raspberry Pi you should populate the following components::


     component |          type          | notes
    ========================================================
     J2        | micro USB connector    |
     U1        | CH340g                 |
     Y1        | 12MHz crystal          |
     C1,C2     | 22pF 0805 SMD caps     | probably optional
     R2        | 10K 0805 SMD resistor  | optional
     D1        | 0805 LED               | optional
     J5        | solder bridge          | bridge
     J4        | solder bridge          | MUST BE OPEN

If you want to power it from the same cable, you will also need these::

     component |          type          | notes
    ========================================================
     C4        | 22u SMD cap            |
     SW1       | Switch                 | or bridge 1-2 for permanent power



Full 5.0v mode
~~~~~~~~~~~~~~~

If you are using this as a stand-alone USB-to-serial converter and WITHOUT a raspberry pi
and want to have 5.0v transmit and receive signals you will need to bridge the 5.0 and 3.3 rails::

     component |          type          | notes
    ========================================================
     J5        | solder bridge          | MUST BE OPEN
     J4        | solder bridge          | bridge



Local 3.3v mode
~~~~~~~~~~~~~~~

If you instead want to use a locally generated 3.3v::

     component |          type          | notes
    ========================================================
     J5        | solder bridge          | MUST BE OPEN
     J4        | solder bridge          | MUST BE OPEN
     U2        | 3.3v SMD regulator     |
     C3, C5    | 100n 0805 SMD caps     |



Remaining components
~~~~~~~~~~~~~~~~~~~~

The following components are not needed and should not be populated::

     component |          type          | notes
    ========================================================
     D4        | protection SMD didoe   | protection for cheap regulators
     R3, R4    | 10K 0805 SMD resistors | for RX/TX LED
     D2, D3    | 0805 SMD LEDs          | RX/TX LED

