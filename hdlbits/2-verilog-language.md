# Verilog Language
- [Basics](#basics)
  - [Simple Wire](#wire)
  - [Four Wires](#wire4)
  - [Inverter](#notgate)
  - [AND Gate](#andgate)
  - [NOR Gate](#norgate)
  - [XNOR Gate](#xnorgate)
  - [Declaring Wires](#wire_decl)
  - [7458 Chip](#7458)
- [Vectors](#vectors)
  - [Vectors](#vector0)
  - [Vectors in More Detail](#vector1)
  - [Vector Part Select](#vector2)
  - [Bitwise Operators](#vectorgates)
  - [Four-Input Gates](#gates4)
  - [Vector Concatenation Operator](#vector3)
  - [Vector Reversal 1](#vectorr)
  - [Replication Operator](#vector4)
  - [More Replication](#vector5)
- [Modules: Hierarchy](#modules-hierarchy)
  - [Modules](#module)
  - [Connecting Ports by Position](#module_pos)
  - [Connecting Ports by Name](#module_name)
  - [Three Modules](#module_shift)
  - [Modules and Vectors](#module_shift8)
  - [Adder 1](#module_add)
  - [Adder 2](#module_fadd)
  - [Carry-Select Adder](#module_cseladd)
  - [Adder-Subtractor](#module_addsub)
  - [](#)

# Worked Examples 

## Basics

### Wire
https://hdlbits.01xz.net/wiki/Wire

```systemverilog
module top_module( input in, output out );
    
	assign out = in;
    
endmodule
```

### Wire4
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

### Notgate
https://hdlbits.01xz.net/wiki/Notgate

```systemverilog
module top_module( input in, output out );
    
	assign out = ~in;
    
endmodule
```

### Andgate
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

### Norgate
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

### Xnorgate
https://hdlbits.01xz.net/wiki/Xnorgate

```systemverilog
module top_module( 
    input a, 
    input b, 
    output out );
    
    assign out = ~(a ^ b);

endmodule
```

### Wire_decl
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

### 7458
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

### Vector0
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

### Vector1
https://hdlbits.01xz.net/wiki/Vector1

```systemverilog
module top_module( 
    input wire [15:0] in,
    output wire [7:0] out_hi,
    output wire [7:0] out_lo );
    
    assign {out_hi, out_lo} = in;

endmodule
```

### Vector2
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

### Vectorgates
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

### Gates4
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

### Vector3
https://hdlbits.01xz.net/wiki/Vector3

```systemverilog
module top_module (
    input [4:0] a, b, c, d, e, f,
    output [7:0] w, x, y, z );//

    // assign { ... } = { ... };
    assign {w, x, y, z} = {a, b, c, d, e, f, 2'b11};

endmodule
```

### Vectorr
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

### Vector4
https://hdlbits.01xz.net/wiki/Vector4

```systemverilog
module top_module (
    input [7:0] in,
    output [31:0] out );//

    // assign out = { replicate-sign-bit , the-input };
    assign out = {{24{in[7]}}, in};

endmodule
```

### Vector5
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
## Modules: Hierarchy

### Module
https://hdlbits.01xz.net/wiki/Module

```systemverilog
module top_module ( input a, input b, output out );
    
    /* Writing it by name means that even if positions are changed, the module 
    call will still be correct */
    mod_a instance2(.in1(a), .in2(b), .out(out));

endmodule
```

### Module_pos
https://hdlbits.01xz.net/wiki/Module_pos

```systemverilog
module top_module ( 
    input a, 
    input b, 
    input c,
    input d,
    output out1,
    output out2
);
    
    mod_a instance1(
        out1, 
        out2, 
        a, 
        b, 
        c, 
        d
    );

endmodule
```

### Module_name
https://hdlbits.01xz.net/wiki/Module_name

```systemverilog
module top_module ( 
    input a, 
    input b, 
    input c,
    input d,
    output out1,
    output out2
);
    mod_a instance_1(
        .out1(out1),
        .out2(out2),
        .in1(a),
        .in2(b),
        .in3(c),
        .in4(d)
    );

endmodule
```

### Module_shift
https://hdlbits.01xz.net/wiki/Module_shift

```systemverilog
module top_module ( input clk, input d, output q );
    
    wire dff12, dff23;
    
    my_dff dff1(
        .clk(clk), 
        .d(d), 
        .q(dff12)
    	);
    
    my_dff dff2(
        .clk(clk), 
        .d(dff12), 
        .q(dff23)
    );
    
    my_dff dff3(
        .clk(clk),
        .d(dff23),
        .q(q)
    );

endmodule
```

### Module_shift8
https://hdlbits.01xz.net/wiki/Module_shift8

```systemverilog
module top_module ( 
    input clk, 
    input [7:0] d, 
    input [1:0] sel, 
    output [7:0] q 
);
    
    wire [7:0] dff1_out, dff2_out, dff3_out;
    
    my_dff8 dff8_1(clk, d, dff1_out);
    my_dff8 dff8_2(clk, dff1_out, dff2_out);
    my_dff8 dff8_3(clk, dff2_out, dff3_out);
    
    /* 4-to-1 MUX in combinational always block. */
    always @(*) begin
        case (sel)
            2'b00	: q = d;
            2'b01	: q = dff1_out;
            2'b10	: q = dff2_out;
            default	: q = dff3_out;
        endcase
    end
    
endmodule
```

### Module_add
https://hdlbits.01xz.net/wiki/Module_add

```systemverilog
module top_module(
    input [31:0] a,
    input [31:0] b,
    output [31:0] sum
);
    wire c;
    
    /* Good idea to screenshot and work backwards for this one. */
    add16 add16_1(a[15:0], b[15:0], 1'b0, sum[15:0], c);
    add16 add16_2(a[31:16], b[31:16], c, sum[31:16], 1'b0);

endmodule
```

### Module_fadd
https://hdlbits.01xz.net/wiki/Module_fadd

```systemverilog
module top_module (
    input [31:0] a,
    input [31:0] b,
    output [31:0] sum
);//
    wire c, cX;
    
    add16 add16_1(a[15:0], b[15:0], 1'b0, sum[15:0], c);
    add16 add16_2(a[31:16], b[31:16], c, sum[31:16], cX);

endmodule

module add1 ( input a, input b, input cin,   output sum, output cout );

// Full adder module here
    assign sum = a ^ b ^ cin;
    assign cout = a&b | a&cin | b&cin;
    
endmodule
```

### Module_cseladd
https://hdlbits.01xz.net/wiki/Module_cseladd

```systemverilog
module top_module(
    input [31:0] a,
    input [31:0] b,
    output [31:0] sum
);
    wire cout_sel, cout2a, cout2b;
    wire [15:0] outa, outb;
    
    add16 add16_1(a[15:0], b[15:0], 1'b0, sum[15:0], cout_sel);
    add16 add16_2a(a[31:16], b[31:16], 1'b0, outa, cout2a);
    add16 add16_2b(a[31:16], b[31:16], 1'b1, outb, cout2b);
    
    // MUX
    always @ (cout_sel, outa, outb) begin
        case (cout_sel)
            1'b0	:	sum[31:16] = outa;
            default	:	sum[31:16] = outb;
        endcase
    end

endmodule
```

### Module_addsub
https://hdlbits.01xz.net/wiki/Module_addsub

```systemverilog
module top_module(
    input [31:0] a,
    input [31:0] b,
    input sub,
    output [31:0] sum
);
    wire c12, cout_2;
    wire [31:0] b_xor;
    
    add16 add16_1(a[15:0], b_xor[15:0], sub, sum[15:0], c12);
    add16 add16_2(a[31:16], b_xor[31:16], c12, sum[31:16], cout_2);

    always @ (b, sub, b_xor) begin
        case (sub)
            1'b0	:	b_xor = b;
            default	:	b_xor = ~b;
        endcase
    end
    
endmodule
```

### 
https://hdlbits.01xz.net/wiki/

```systemverilog

```
