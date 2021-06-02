<h2>ESP 32 Disassembler</h2>

<p>This is an ambitious project: to make a disassembler for the ESP32 binary code.</p>
<p>Because, before designing an ESP32 assembler, you have to understand the ESP32 code. And the best way is to create an ESP32 disassembler.</p>
<p>To test this disassembler, run gForth:</p>
<pre>gforth Disassembler.txt</pre>
<p>The code will be compiled by gForth.</p>


<p>Execution of <b>dispINTSRs</b>:</p>

<pre>defined ESP32 instructions:
  600100 ABS       RRR     Absolute Value
  fa0010 ABS.S     RRR     Absolute Value Single
  800000 ADD       RRR     Add
    000a ADD.N     RRRN    Narrow Add
  0a0000 ADD.S     RRR     Add Single
    000b ADDI.N    RRRN    Narrow Add Immediate
  900000 ADDX2     RRR     Add with Shift by 1
  a00000 ADDX4     RRR     Add with Shift by 2
  b00000 ADDX8     RRR     Add with Shift by 3
  009000 ALL4      RRR     All 4 Booleans True
  00b000 ALL8      RRR     All 8 Booleans True
  100000 AND       RRR     Bitwise Logical And</pre>

