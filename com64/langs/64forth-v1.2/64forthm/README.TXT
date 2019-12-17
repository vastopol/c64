64-FORTH for the C64
--------------------
64-FORTH is a cartridge for the Commodore 64. It was
written by Tom Zimmer and published by HES in 1983.

64-FORTH is a super-set of fig-FORTH. It uses the
Commodore file-system and has many functions that
access the C64 hardware including sound and graphics.
The cartridge occupies 16k of memory from $8000-BFFF.

64-FORTH was provided with a comprehensive manual.
It is enclosed here as a plain ASCII text file -
64FORTH.TXT.

Sadly I no longer have the cartridge, so am unable
to include the binary of the program.


The following describes a patch which can be made to
the program to allow 64-FORTH to be 'soft-loaded' i.e.
loaded into memory and run like any other program!


64-FORTH SOFTLOAD MODIFICATIONS   27/7/85
-----------------------------------------

1. SWITCH BASIC OUT

   .: 8027 A9 36 85 01     (REPLACES 'NOP'S )

   LDA #$36
   STA $01

2. PREVENT FORTH FROM SWITCHING IN BASIC

   .: A765 36              (.:A765 37 )

3. PREVENT ERASURE OF $8000 - $83FF

   .: 93F5 D4 86           (REPLACES 'ERASE' WITH '2DROP')

4. PREVENT RESET FROM CORRUPTING $A000

   .: 8021 EA EA EA        (DISABLE RAMTAS ROUTINE $FD50 )

5. COMPUTE NEW CHECKSUM

   .: 9389 F2 82

6. ORIGINAL VALUES

   .: 8021 20 50 FD
   .: 8027 EA EA EA EA
   .: 9389 E4 83
   .: 93F5 45 8E
   .: A765 37

