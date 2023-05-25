# casio-pro-101-info
Information about the Casio PRO-101 calculator

Internal program Structure
--------------------------

By looking at the RAM contents some information about the structure of a program within RAM can
be determined.

Components
----------

The TC5006P is a 1024 x 1 bit CMOS RAM. There's no information about it on the internet that I can find, but 
from signal traces and oscilloscope probing it looks like it has the same pinout as the TC5508 RAM chip that Toshiba
made a bit later than the TC5006P.

HD36106
-------

This device appears to be a 1024 bit RAM chip. It seems to be a device where some address lines are set up and then the data is clocked out by a clock (two phase) in a multi-bit sequence.

<code>

  Pinout
  
  1   VA
  2   VB  
  3   nc
  4   nc
  5   CLKA    (VB levels)
  6   CLKB    (VB levels)
  7   A3      (VA levels)
  8   0V
  9   A2
  10  A1
  11  A0
  12  CE      (VA levels)
  13  RW      (VA levels)
  14  DOUT    (VA levels)
  15  DIN     (VA levels)
  16  0V
 
  VA is -6.6V in the PRO-101
  VB is -14.4V in the PRO-101
  
  
