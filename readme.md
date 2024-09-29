# Instalation
```bash
 sudo apt install iverilog gtkwave
```

# Project setup
1. Make a directory in project name (exorGate)
2. Create a .v code file (exorGate.v)
   ``` verilog
   module exorGate (
          input a_i,
          input b_i,
          output c_o
   );
   assign c_o=a_i^b_i;
   endmodule
   ```
3. Create a _tb.v testbench file (exorGate_tb.v)
   ``` verilog
   `timescale 1ns/100ps
   modeule exorGate_tb;

   reg a;
   reg b;
   wire c;

   exorGate u0_DUT (
                    .a_i(a),
                    .b_i(b),
                    .c_o(c)
                    );

   initial begin
   $dumpfile("testexor.vcd");
   $dumpvars(0,exorGate_tb);

         a=1'b0;b=1'b0;
   #10   a=1'b0;b=1'b1;
   #10   a=1'b1;b=1'b0;
   #10   a=1'b1;b=1'b1;

   #200 $finish;
   endmodule
   ```
4. Combile using iverilog
   ```bash
   iverilog exorGate.v exorGate_tb.v -o exor_wav
   ```
5. Generate waveform
   ```bash
   vvp exor_wave
   ```
6. Open in gtkwave to see o/p wave
   ```bash
   gtkwave test_exor.vcd
   ```
