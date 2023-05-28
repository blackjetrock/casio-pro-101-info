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
  
  HD36106 Data format
  ===================
  
  Data is a 128bit sequence. CE is low for 128 CLKs but data is only in the lower 64 bits. These are clocked out first. For example:
  
  Addr:D DAT:05000000070000043007001234567890 RW:FFFFFFFFFFFFFFFF0000000000000000
  
  The first bit to be clocked out is at the right hand end of the data as shown here. That puts the digits in the correct order. The RW signal is low for the 64 bits of data if that data is to be written. The HD36106 has a data in pin and a data out pin, the data shown her eis the data in pin data.
  The address is the address of the 'program memory' of the PRO-101, it has 15 of these, so addresses 1 to 15 inclusive (1-F in hex) are valid. 
  
  The data:
  
  DAT:05000000070000043007001234567890
  
  can be broken up as:
  
  DAT:0500000007000004 300 7 00 1234567890
    
  1234567890    is the register value that is being written. This is the 10 digit BCD that 
                the PRO-101 supports. Exponents aren't supported on the PRO-101.
  00            unknown
  7             Position of decimal point
  300           unknown
  
  0500000007000004  Fixed unknown data
  
  
  Indirect Register I
  ===================
  
  The indirect register (I) is not stored in the HD36106. This means that some storage must be in the processor IC.
  
   Memory (M+,M-,MR,MC, etc...)
  =============================
  
  This memory also does not appear to be stored in the HD36106. 
  
