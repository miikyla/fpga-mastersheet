### Verilog Language

## Basics

# Simple Wire
https://hdlbits.01xz.net/wiki/Wire

```systemverilog
module top_module( input in, output out );
    
	assign out = in;
    
endmodule
```

# Four Wires
https://hdlbits.01xz.net/wiki/Wire4

```systemverilog
module top_module( 
    input a,b,c,
    output w,x,y,z );
    
    /* Can concatenate both the input and output easily to arrays since they're 
       explicitly defined in the problem. */
    assign {w,x,y,z} = {a,b,b,c};

endmodule
```

# Inverter
https://hdlbits.01xz.net/wiki/Notgate

```systemverilog
module top_module( input in, output out );
    
	assign out = ~in;
    
endmodule
```

# AND Gate
https://hdlbits.01xz.net/wiki/Andgate

```systemverilog
module top_module( 
    input a, 
    input b, 
    output out );
    
    /* Choosing a bitwise AND (&) since output out is declared as a single bit 
       output (and bitwise AND will reduce the output to a single bit). Doesn't 
       matter in this example but it would if the inputs were multi-bit. */
    assign out = a & b;

endmodule
```

# NOR Gate
https://hdlbits.01xz.net/wiki/Norgate

```systemverilog
module top_module( 
    input a, 
    input b, 
    output out );
    
    /* As in the previous example, choosing a bitwise OR since the output is 
       declared as a single bit. */
    assign out = ~(a | b);

endmodule
```

# XNOR Gate
https://hdlbits.01xz.net/wiki/Xnorgate

```systemverilog
module top_module( 
    input a, 
    input b, 
    output out );
    
    assign out = ~(a ^ b);

endmodule
```

# Declaring Wires
https://hdlbits.01xz.net/wiki/Wire_decl

```systemverilog
module top_module(
    input a,
    input b,
    input c,
    input d,
    output out,
    output out_n   ); 
    
    wire and1, and2;
    
    assign and1 = a & b;
    assign and2 = c & d;
    
    assign out = and1 | and2;
    assign out_n = ~out;

endmodule
```

# 7458 Chip
https://hdlbits.01xz.net/wiki/7458

```systemverilog
module top_module ( 
    input p1a, p1b, p1c, p1d, p1e, p1f,
    output p1y,
    input p2a, p2b, p2c, p2d,
    output p2y );
    
    /* I personally prefer screenshotting these types of problems, working 
       backwards from the output and highlighting the sections that I've already 
       written code for. */
    assign p1y = (p1a & p1c & p1b) | (p1d & p1e & p1f);
    assign p2y = (p2c & p2d) | (p2a & p2b);


endmodule
```