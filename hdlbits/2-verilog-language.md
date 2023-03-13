# Verilog Language

## Basics

### Simple Wire
https://hdlbits.01xz.net/wiki/Wire

```systemverilog
module top_module( input in, output out );
    
	assign out = in;
    
endmodule
```

### Four Wires
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

### Inverter
https://hdlbits.01xz.net/wiki/Notgate

```systemverilog
module top_module( input in, output out );
    
	assign out = ~in;
    
endmodule
```

### AND Gate
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

### NOR Gate
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

### XNOR Gate
https://hdlbits.01xz.net/wiki/Xnorgate

```systemverilog
module top_module( 
    input a, 
    input b, 
    output out );
    
    assign out = ~(a ^ b);

endmodule
```

### Declaring Wires
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

### 7458 Chip
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

## Vectors

### Vectors
https://hdlbits.01xz.net/wiki/Vector0

```systemverilog
module top_module ( 
    input wire [2:0] vec,
    output wire [2:0] outv,
    output wire o2,
    output wire o1,
    output wire o0  );
    
    assign outv = vec;
    assign {o2, o1, o0} = vec;

endmodule
```

### Vectors in More Detail
https://hdlbits.01xz.net/wiki/Vector1

```systemverilog
module top_module( 
    input wire [15:0] in,
    output wire [7:0] out_hi,
    output wire [7:0] out_lo );
    
    assign {out_hi, out_lo} = in;

endmodule
```

### Vector Part Select
https://hdlbits.01xz.net/wiki/Vector2

```systemverilog
module top_module( 
    input [31:0] in,
    output [31:0] out );//

    // assign out[31:24] = ...;
    assign {out[31:24], out[23:16], out[15:8], out[7:0]} = {in[7:0], in[15:8],
    in[23:16], in[31:24]};

endmodule
```

### Bitwise Operators
https://hdlbits.01xz.net/wiki/Vectorgates

```systemverilog
module top_module( 
    input [2:0] a,
    input [2:0] b,
    output [2:0] out_or_bitwise,
    output out_or_logical,
    output [5:0] out_not
);
    
    assign out_or_bitwise = a | b;
    assign out_or_logical = a || b;
    assign out_not = {~b, ~a};

endmodule
```
### Four-Input Gates
https://hdlbits.01xz.net/wiki/Gates4

```systemverilog
module top_module( 
    input [3:0] in,
    output out_and,
    output out_or,
    output out_xor
);
    assign out_and 	= &in;
    assign out_or 	= |in;
    assign out_xor 	= ^in;

endmodule
```

### Vector Concatenation Operator
https://hdlbits.01xz.net/wiki/Vector3

```systemverilog
module top_module (
    input [4:0] a, b, c, d, e, f,
    output [7:0] w, x, y, z );//

    // assign { ... } = { ... };
    assign {w, x, y, z} = {a, b, c, d, e, f, 2'b11};

endmodule
```

### Vector Reversal 1
https://hdlbits.01xz.net/wiki/Vectorr

```systemverilog
module top_module( 
    input [7:0] in,
    output [7:0] out
);
    
    generate
        genvar i;
        for (i = 0; i < 8; i = i + 1) begin: flip_wires_block
            assign out[i] = in[7-i];
        end
    endgenerate
  
endmodule
```

### Replication Operator
https://hdlbits.01xz.net/wiki/Vector4

```systemverilog
module top_module (
    input [7:0] in,
    output [31:0] out );//

    // assign out = { replicate-sign-bit , the-input };
    assign out = {{24{in[7]}}, in};

endmodule
```

### More Replication
https://hdlbits.01xz.net/wiki/Vector5

```systemverilog
module top_module (
    input a, b, c, d, e,
    output [24:0] out );//

    // The output is XNOR of two vectors created by 
    // concatenating and replicating the five inputs.
    // assign out = ~{ ... } ^ { ... };
    assign out = ~{5{a, b, c, d, e}} ^ {{5{a}}, {5{b}}, {5{c}}, {5{d}}, {5{e}}};
    
endmodule
```

```systemverilog

```