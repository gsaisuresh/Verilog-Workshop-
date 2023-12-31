# Verilog-Workshop
This is part of Verilog Workshop organised by vlsideepdive. Here I include the lab programs which I did in workshop. ModelSim is used for Simulation and Quartus Prime is used for synthesis. 

## Table of Contents
1. [Day-01 Labs](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#day-01-labs)
    - [DataFlow based Design and Testbench for one bit half adder in Verilog](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#dataflow-based-design-and-testbench-for-one-bit-half-adder-in-verilog)
    - [Behavioral Design and Testbench for one bit half adder in Verilog](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#behavioral-design-and-testbench-for-one-bit-half-adder-in-verilog)
    - [Structural Design and Testbench for one bit half adder in Verilog](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#structural-design-and-testbench-for-one-bit-half-adder-in-verilog)
    - [DataFlow based Design and Testbench for one bit full adder in Verilog](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#dataflow-based-design-and-testbench-for-one-bit-full-adder-in-verilog)
    - [Behavioral Design and Testbench for one bit full adder in Verilog](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#behavioral-design-and-testbench-for-one-bit-full-adder-in-verilog)
    - [Structural Design and Testbench for one bit full adder in Verilog using primitives](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#structural-design-and-testbench-for-one-bit-full-adder-in-verilog-using-primitives)
    - [Structural Design and Testbench for one bit full adder in Verilog using HalfAdder](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#structural-design-and-testbench-for-one-bit-full-adder-in-verilog-using-halfadder)
    - [Verilog code which shows usage of all operators with $display statement](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#verilog-code-which-shows-usage-of-all-operators-with-display-statement)
      - [Bitwise Operators](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#bitwise-operators)
      - [Logical Operators](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#logical-operators)
      - [Arithmetic Operators](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#arithmetic-operators)
      - [Equality Operators](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#equality-operators)
      - [Relational Operators](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#relational-operators)
      - [Shift Operators](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#shift-operators)
      - [Concatenation Operator](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#concatenation-operator)
    - [Create a verilog task for conversion of Celsius into Fahrenheit]

2. [Day-02 Labs](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#day-02-lab)
    - [Dataflow based Design and Testbench for 4 bit full adder in Verilog](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#dataflow-based-design-and-testbench-for-4-bit-full-adder-in-verilog)
    - [Design and Testbench for 2:1 Mux in Verilog](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#design-and-testbench-for-21-mux-in-verilog)
    - [Design and Testbench for 4:1 Mux in Verilog](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#design-and-testbench-for-41-mux-in-verilog)
    - [Design and Testbench 2×4 Decoder in Verilog](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#design-and-testbench-24-decoder-in-verilog)
    - [Design and Testbench 4×2 Encoder in Verilog]
    - [Design and Testbench 4×2 Priority Encoder in Verilog]
    - [Design and Testbench 4 bit comparator in Verilog]
    - [Design and Testbench 8 bit barrel shifter in Verilog]
    - [Design and Testbench ALU in Verilog]

## Day-01 Labs

### DataFlow based Design and Testbench for one bit half adder in Verilog

#### Verilog Code 
```
module half_adder_d(a,b,s,c);
	input a,b;
	output s,c;
	assign s=a^b;
	assign c=a&b;
endmodule
```

#### Testbench code
```
module half_adder_dtb;
	reg a,b;
	wire s,c;
	
	half_adder_d DUT(a,b,s,c);
	
	initial 
		begin
			$monitor("time=%d, a=%b, b=%b, sum=%b, carry=%b", $time, a,b,s,c);
			a=0; b=0;
			#10 b=1;
			#10 a=1; b=0;
			#10 b=1;
			#10 $finish;
		end
endmodule
```

#### ModelSim Simulation Result 

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/a8bfe89c-ff03-42c9-944f-4f8ca2c6fd93)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/4e8424fd-81fa-49e0-91f3-2e6a24873762)

#### Quartus Prime Synthesis Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/f3f0e37d-c047-4079-b8f1-5999091437f0)

### Behavioral Design and Testbench for one bit half adder in Verilog

#### Verilog code
```
module half_adder_b(input a, input b, output reg sum, output reg carry);
	always@(a,b)
		begin
			sum = a^b;
			carry = a&b;
		end
endmodule
```

#### Testbench code
```
module half_adder_btb;
	reg a,b;
	wire sum,carry;
	integer i;
	
	half_adder_b DUT(a,b,sum,carry);
	
	initial 
		begin
			for(i=0;i<4;i=i+1)
				begin
					{a,b} = i;
					#10;
				end
		end
		
	initial 
		$monitor("time=%d, a=%b, b=%b, sum=%b, carry=%b", $time, a,b,sum,carry);

	initial	#50 $finish;
endmodule
```

#### ModelSim Simulation Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/391b4fcf-61f6-4f4a-95f4-00b77bb05113)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/cd11ab8b-a9b6-4de7-831d-35637f1a079c)

#### Quartus Prime Synthesis Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/b5a9d9a2-738e-4d6b-b87c-ebdd9118f9db)

### Structural Design and Testbench for one bit half adder in Verilog

#### Verilog code
```
module half_adder_s(a,b,sum,carry);
	input a,b;
	output sum,carry;
	
	and A1(carry,a,b);
	xor X1(sum,a,b);

endmodule 	
```

#### Testbench code
```
module half_adder_stb;
	reg a,b;
	wire sum,carry;
	integer i;
	
	half_adder_s DUT(a,b,sum,carry);
	
	initial 
		fork
			for(i=0;i<4;i=i+1)
				begin
					{a,b} = i;
					#10;
				end
		$monitor("time=%d, a=%b, b=%b, sum=%b, carry=%b", $time, a,b,sum,carry);
		#40 $finish;
	    join
endmodule
```

#### ModelSim Simulation Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/0618b54a-41d7-4626-bf34-f9463da1aaaa)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/19eb59d5-ac80-48de-8b29-efe68fb6d52e)

#### Quartus Prime Synthesis Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/11187d0b-e2e0-4a26-ae41-501bb3b3a382)

### DataFlow based Design and Testbench for one bit full adder in Verilog

#### Verilog code
```
module full_adder_d(a,b,cin,sum,carry);
	input a,b,cin;
	output sum,carry;
	assign sum = a^b^cin;
	assign carry = (a&b) | (b&cin) | (a&cin) ; 
endmodule 
```

#### Testbench code
```
module full_adder_dtb;
	reg a,b,cin;
	wire sum,carry;
	integer i;
	
	full_adder_d DUT(a,b,cin,sum,carry);
	
	initial 
		begin
			for(i=0;i<8;i=i+1)
				begin
					{a,b,cin} = i;
					#10;
				end
		end
		
	initial 
		$monitor("time=%d, a=%b, b=%b, carryin=%b, sum=%b, carry=%b", $time, a,b,cin,sum,carry);

	initial	#100 $finish;
	
endmodule
```

#### ModelSim Simulation Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/548a2e64-312f-43c6-877e-5cb91095a34e)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/0165743d-cc26-48dd-93a5-e45758841aff)

#### Quartus Prime Synthesis Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/459fcfe4-fc2d-4f2a-b64d-0676f63a904e)

### Behavioral Design and Testbench for one bit full adder in Verilog

#### Verilog code
```
module full_adder_b(input a, input b, input cin, output reg sum, output reg carry);
	always@(*)
		begin
			sum = a^b^cin;
			carry = (a&b) | (b&cin) | (a&cin) ;
		end
endmodule 
```

#### Testbench code
```
module full_adder_btb;
	reg a,b,cin;
	wire sum,carry;
	integer i;
	
	full_adder_b DUT(a,b,cin,sum,carry);
	
	initial 
		fork
			for(i=0;i<8;i=i+1)
				begin
					{a,b,cin} = i;
					#10;
				end
		$monitor("time=%d, a=%b, b=%b, carryin=%b, sum=%b, carry=%b", $time, a,b,cin,sum,carry);
		#90 $finish;
		join
endmodule
```

#### ModelSim Simulation Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/0456802b-1123-4528-aa75-59dd5e1b0679)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/0f4c939e-069c-4b24-a5fa-de39cfd96e09)

#### Quartus Prime Synthesis Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/95522b96-73b1-4787-8036-89382adb8061)

### Structural Design and Testbench for one bit full adder in Verilog using primitives

#### Verilog code
```
module full_adder_s(input a,b,cin, output sum,carry);
	
	wire n1,n2,n3;
	xor X1(sum,a,b,cin);
	and A1(n1,a,b);
	and A2(n2,b,cin);
	and A3(n3,a,cin);
	or O1(carry,n1,n2,n3);
	
endmodule
```

#### Testbench code
```
module full_adder_stb;
	reg a,b,cin;
	wire sum,carry;
	integer i;
	
	full_adder_s DUT(a,b,cin,sum,carry);
	
	initial 
		fork
			for(i=0;i<8;i=i+1)
				begin
					{a,b,cin} = i;
					#10;
				end
		$monitor("time=%d, a=%b, b=%b, carryin=%b, sum=%b, carry=%b", $time, a,b,cin,sum,carry);
		#80 $finish;
		join
endmodule
```

#### ModelSim Simulation Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/13cf2668-c932-4083-924b-84e08f800921)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/dac31f90-49e6-4c4a-baa6-a939b1eabb5e)

#### Quartus Prime Synthesis Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/a19b4128-32ef-46f5-b1c5-de2c7b4ca675)

### Structural Design and Testbench for one bit full adder in Verilog using HalfAdder

#### Verilog Code 
```
module full_adder_sha(input a,b,cin, output sum,carry);
	wire n1,n2,n3;
	
	half_adder_d HA1(a,b,n1,n2);
	half_adder_d HA2(n1,cin,sum,n3);
	or O1(carry,n2,n3);

endmodule
```

#### Testbench code
```
module full_adder_shatb;
	reg a,b,cin;
	wire sum,carry;
	
	full_adder_sha DUT(a,b,cin,sum,carry);
	
	task initialization;
		begin 
			{a,b,cin} = 0;
		end
	endtask
	
	task inputs(input [2:0]X);
		begin
			{a,b,cin} = X;
		end
	endtask
	
	initial 
		begin
			initialization;
			#10;
			inputs(3'b001);
			#10;
			inputs(3'b010);
			#10;
			inputs(3'b011);
			#10;
			inputs(3'b100);
			#10;
			inputs(3'b101);
			#10;
			inputs(3'b110);
			#10;
			inputs(3'b111);
			#10;
		end
	
	initial
	$monitor("time=%d, a=%b, b=%b, carryin=%b, sum=%b, carry=%b", $time, a,b,cin,sum,carry);
		
	initial	#90 $finish;	

endmodule
```

#### ModelSim Simulation Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/5f455949-d3b1-447f-975e-87cd92dcfb5a)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/a5f29bef-456b-4bc9-af30-f5b8e990dd8f)

#### Quartus Prime Synthesis Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/4d6d9874-374e-49d6-8c0f-5ab114ace0d0)

#### Verilog code which shows usage of all operators with $display statement

#### Bitwise Operators

#### Verilog Code
```
module bitwise_op;
	
	reg [3:0] a,b,c,d;
	reg [3:0] w1,w2,w3,w4,w5,w6,w7,w8;
	reg [3:0] x1,x2,x3,x4,x5,x6,x7,x8,x9;
	
	initial 
		begin
			a=4'b1011; 
			b=4'b0011;
			c=4'b101x;
			d=4'b0x1x;
			
			w1= ~a; w2=~b;
			w3= a&b;
			w5= a | b;
			w7= a^b;
			w8= a ~^ b;
			
			x1= ~c; x2=~d;
			x3= a&c;
			x5= a | c;
			x7= a^c;
			x8= a ~^ c;
			x9= c ^ d;
			
			$display("a=%b, b=%b, w1=%b, w2=%b, w3=%b, w5=%b, w7=%b, w8=%b",a,b,w1,w2,w3,w5,w7,w8);
			$display("c=%b, d=%b, x1=%b, x2=%b, x3=%b, x5=%b, x7=%b, x8=%b, x9=%b",c,d,x1,x2,x3,x5,x7,x8,x9);
		end
endmodule
```

#### ModelSim Result 

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/24536cc9-a705-4431-8d09-b9cfb554850f)

#### Logical Operators

#### Verilog Code
```
module logical_op;

	reg [3:0] a,b,c,d;
	reg w1,w2,w3,w4,w5,w6,w7,w8,w9;
	reg x1,x2,x3,x5,x7,x8,x9;
	
	initial
		begin
			a=4'b1011;
			b=4'b0000;
			c=4'b101x;
			d=4'b000x;
			
			w1=!a; w2=!b; w3=!c; w4=!d;
			w5=a&&b; w6=a&&c; w7=a&&d; w8=b&&c; w9=b&&d;
			x1=a||b; x2=a||c; x3=a||d; x5=b||c; x7=b||d;
			x8=c&&d; x9=c||d; 
			
			$display("a=%b, b=%b, w1=%b, w2=%b, w3=%b, w4=%b, w5=%b, w6=%b, w7=%b, w8=%b, w9=%b",a,b,w1,w2,w3,w4,w5,w6,w7,w8,w9);
			$display("c=%b, d=%b, x1=%b, x2=%b, x3=%b, x5=%b, x7=%b, x8=%b, x9=%b",c,d,x1,x2,x3,x5,x7,x8,x9);
		end
endmodule
```

#### ModelSim Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/f4173d04-bc06-40b6-ba21-def0b68f2c79)

#### Arithmetic Operators

#### Verilog code
```
module arithmetic_op;

	reg [3:0] a,b,c,d,e,f,c1,s,b1,d1,g,b2,d2;
	reg [3:0] w1,w2,w3,w4,w5,w6,w7,w8,w9;
	reg [3:0] x1,x2,x3,x5,x7,x8,x9;
	
	initial
		begin
			a=4'b1011;
			b=4'b0010;
			c=4'b101x;
			d=4'b000x;
			e=4'b1111;
			f=4'b0001;
			g=4'b1100;
			
			{c1,s}=e+f;
			{b1,d1}=g-f;
			{b2,d2}=f-g;
			w1=a+b; w2=a+c; w3=a+d; w4=b+d;
			w5=b+c; w6=c+d; w7=a-b; w8=a-c; w9=b-d;
			x1=a*b; x2=a*c; x3=b*d; x5=a/b; x7=a/d;
			x8=a%b; x9=a%c; 
			
			$display("a=%b, b=%b, w1=%b, w2=%b, w3=%b, w4=%b, w5=%b, w6=%b, w7=%b, w8=%b, w9=%b",a,b,w1,w2,w3,w4,w5,w6,w7,w8,w9);
			$display("c=%b, d=%b, x1=%b, x2=%b, x3=%b, x5=%b, x7=%b, x8=%b, x9=%b",c,d,x1,x2,x3,x5,x7,x8,x9);
			$display("e=%b, f=%b, carry=%b, sum=%b",e,f,c1,s);
			$display("g=%b, f=%b, borrow=%b, diff=%b",g,f,b1,d1);
			$display("f=%b, g=%b, borrow=%b, diff=%b",f,g,b2,d2);
		end
endmodule
```

#### ModelSim Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/3b7e60ac-385f-4d4d-a500-d32cf58c0272)

#### Equality Operators

#### Verilog Code
```
module equality_op;

	reg [3:0] a,b,c,d,e,f,g,h,i,j;
	reg w1,w2,w3,w4,w5,w6,w7,w8,w9;
	reg x1,x2,x3,x5,x7,x8,x9;
	
	initial
		begin
			a=4'b1011;	b=4'b0011;
			c=4'b10x1;	d=4'b00x1;
			e=4'b10z1; f=4'b00z1;
			g=4'b10x1; h=4'b00x1;
			i=4'b10z1; j=4'b00z1;
			
			w1=(a==b); w2=(a==c); w3=(a==e);
			w4=(a!=b); w5=(a!=c); w6=(a!=e);
			w7=(a!==c); w8=(a===c); w9=(a===e);
			x1=(c===e); x2=(d===f); x3=(c!==e);
			x5=(c===g); x7=(d===h); x8=(i===e);
			x9=(f===j);
			
			$display("a=%b ,b=%b ,c=%b ,d=%b ,e=%b ,f=%b ,g=%b ,h=%b ,i=%b ,j=%b",a,b,c,d,e,f,g,h,i,j);
			$display("w1=%b, w2=%b, w3=%b, w4=%b, w5=%b, w6=%b, w7=%b, w8=%b, w9=%b",w1,w2,w3,w4,w5,w6,w7,w8,w9);
			$display("x1=%b, x2=%b, x3=%b, x5=%b, x7=%b, x8=%b, x9=%b",x1,x2,x3,x5,x7,x8,x9);
		end
endmodule
```

#### ModelSim Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/76d8b7e2-c060-4464-b3b4-1d189b99dfcc)

#### Relational Operators

#### Verilog Code
```
module relational_op;
	
	reg [3:0] a,b,c,d,e,f;
	reg w1,w2,w3,w4,w5,w6,w7,w8,w9;
	reg x1,x2,x3;
	
	initial
		begin
			a=4'b1100; b=4'b0011; e=4'b0011; f=4'b1100;
			c=4'b1x0x; d=4'b1z00;
			
			w1=a>b; w2=a<b; w3=a>=b; w4=b>=e; w5=a>=f;
			w6=a>c; w7=a>=c; w8=a>d; w9=a>=d; 
			x1=a<c; x2=a<=c; x3=a<d;
			
			$display("a=%b ,b=%b ,c=%b ,d=%b ,e=%b ,f=%b",a,b,c,d,e,f);
			$display("w1=%b, w2=%b, w3=%b, w4=%b, w5=%b, w6=%b, w7=%b, w8=%b, w9=%b",w1,w2,w3,w4,w5,w6,w7,w8,w9);
			$display("x1=%b, x2=%b, x3=%b",x1,x2,x3);
		end

endmodule
```

#### ModelSim Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/c700b2a5-fae1-469a-ad74-2cf84640aae8)

#### Shift Operators

#### Verilog Code
```
module shift_op;

	reg [3:0] a,b,c,d,e,f;
	reg signed [3:0] a1,b1,c1,d1,e1,f1;
	reg [3:0] w1,w2,w3,w4,w5,w6,w7,w8,w9,w10,w11,w12;
	reg [3:0] x1,x2,x3,x4,x5,x6,x7,x8,x9,x10,x11,x12;
	reg [3:0] y1,y2,y3,y4,y5,y6,y7,y8,y9,y10,y11,y12;
	
	initial 
		begin
			a=4'b1011; b=4'b0011; c=4'b10x1; d=4'bxx01; e=4'bzz01; f=4'bxxxx;
			a1=4'sb1011; b1=4'sb0011; c1=4'sb10x1; d1=4'sbxx01; e1=4'sbzz01; f1=4'sbxxxx;
			//logical shift operators
			w1=a<<1; w2=a>>1; w3=b<<1; w4=b>>1; w5=c<<1; w6=c>>1; w7=d>>1; w8=d<<1; w9=e<<1; w10=e>>1; w11=f<<1; w12=f>>1;
			
			//arithmetic operators
			x1=a<<<1; x2=a>>>1; x3=b<<<1; x4=b>>>1; x5=c<<<1; x6=c>>>1; x7=d>>>1; x8=d<<<1; x9=e<<<1; x10=e>>>1; x11=f<<<1; x12=f>>>1;
			
			y1=a1<<<1; y2=a1>>>1; y3=b1<<<1; y4=b1>>>1; y5=c1<<<1; y6=c1>>>1; y7=d1>>>1; y8=d1<<<1; y9=e1<<<1; y10=e1>>>1; y11=f1<<<1; y12=f1>>>1;
			
			$display("a=%b ,b=%b ,c=%b ,d=%b ,e=%b ,f=%b",a,b,c,d,e,f);
			$display("a1=%b ,b1=%b ,c1=%b ,d1=%b ,e1=%b ,f1=%b",a1,b1,c1,d1,e1,f1);
			$display("w1=%b, w2=%b, w3=%b, w4=%b, w5=%b, w6=%b, w7=%b, w8=%b, w9=%b, w10=%b, w11=%b, w12=%b",w1,w2,w3,w4,w5,w6,w7,w8,w9,w10,w11,w12);
			$display("x1=%b, x2=%b, x3=%b, x4=%b, x5=%b, x6=%b, x7=%b, x8=%b, x9=%b, x10=%b, x11=%b, x12=%b",x1,x2,x3,x4,x5,x6,x7,x8,x9,x10,x11,x12);
			$display("y1=%b, y2=%b, y3=%b, y4=%b, y5=%b, y6=%b, y7=%b, y8=%b, y9=%b, y10=%b, y11=%b, y12=%b",y1,y2,y3,y4,y5,y6,y7,y8,y9,y10,y11,y12);
		end
endmodule
```

#### ModelSim Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/e856510c-8b85-46e4-9117-90732a75f2e8)

#### Concatenation Operator

#### Verilog Code
```
module concat_op;

	reg [3:0] a,b,c,d,e,f,g;
	reg [11:0] h,i,j,k,l,m;
	
	initial 
		begin
			a=4'b1011; b=4'd2; c=4'bx1; d=4'bz0; e='h11; f='ozx0; g=4'b?0?;
			
			h={a,b,c}; 			i={c,d};
			j={e,f};			k={3{g}};
			l={h[11:9],{2{a}}}; m={{3{c}},{3{d}},j[11:9]};
			
			$display("a=%b, b=%b, c=%b, d=%b, e=%b, f=%b, g=%b",a,b,c,d,e,f,g);
			$display("h=%b, i=%b, j=%b, k=%b, l=%b, m=%b",h,i,j,k,l,m);
		end
endmodule
```

#### ModelSim Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/0ade1675-11d7-4988-a40e-c55feb780b80)



## Day-02 Lab

### Dataflow based Design and Testbench for 4 bit full adder in Verilog

#### Verilog Code 
```
module four_bit_adder_d(a,b,cin,sum,carryout);
	input [3:0]a,b;
	input cin;
	output [3:0]sum;
	output carryout;
	
	assign {carryout,sum} = a+b+cin;
	
endmodule
```

#### Testbench code
```
module four_bit_adder_dtb();
	reg [3:0]a,b;
	reg cin;
	wire [3:0]sum;
	wire carryout;
	
	four_bit_adder_d DUT(a,b,cin,sum,carryout);
	
	initial 
		$monitor("time = %d, a=%b, b=%b, cin=%b, sum=%b, carryout=%b",$time,a,b,cin,sum,carryout);
		
	initial
		begin	
		{a,b,cin}=3'b000;
		
		repeat(16)
			begin
				#10 a=a+1;
				repeat(16)
					begin	
						#10 b=b+1;
						repeat(2)
							#10 cin=~cin;
					end
			end
		end
		
	initial #450 $finish;
	
endmodule
```

#### ModelSim Simulation Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/f2d2970b-88bb-4a12-950b-e9ddae55d439)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/c64b7755-6e0b-4875-8628-8ed3c3fd1b4e)

#### Quartus Prime Synthesis Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/85527631-8eb1-4680-ae06-bd547f5ad750)

### Design and Testbench for 2:1 Mux in Verilog

#### Model-1 : 2:1 Mux Dataflow Modelling

#### Verilog code
```
module mux_2_1_d (input [1:0]I,input S, output Y);

	assign Y = S ? I[1] : I[0];
	
endmodule 
```

#### Testbench code
```
module mux_2_1_dtb;
	reg [1:0] I;
	reg S;
	wire Y;
	
	mux_2_1_d DUT(I,S,Y);
	
	task inputs(input [1:0]A,input B);
		begin
			{I,S} = {A,B};
		end
	endtask
	
	initial
		begin
			inputs(2'b00,0);
			#10;
			inputs(2'b01,0);
			#10;
			inputs(2'b10,1);
			#10;
			inputs(2'b00,1);
			#10;
		end
	
	initial
		$monitor("time=%d, I=%b, S=%b, Y=%b",$time,I,S,Y);
		
	initial #50 $finish;
endmodule
```

#### ModelSim Simulation Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/7efff2f3-7bbb-4c66-bdd8-105b99a99d9d)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/42a6624e-05c4-4065-9639-c5b043e20ed9)

#### Quartus Prime Synthesis Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/37e79483-4213-4a17-bd50-e67a37fb76a9)

#### Model-2 : 2:1 Mux Behavioral Modelling

#### Verilog Code
```
module mux_2_1_b(I,S,Y);
	input [1:0]I;
	input S;
	output reg Y;
	
	always@(*)
		begin
			if(S) 
				Y = I[1];
			else
				Y = I[0];
	    end
			
endmodule
```

#### Testbench code
```
module mux_2_1_btb;
	reg [1:0] I;
	reg S;
	wire Y;
	integer i;
	
	mux_2_1_b DUT(I,S,Y);
	
	initial
		begin
			for(i=0;i<8;i=i+1)
				begin
					{I,S}=i;
					#10;
				end
		end
	
	initial
		$monitor("time=%d, I=%b, S=%b, Y=%b",$time,I,S,Y);
		
	initial #80 $finish;
endmodule
```

#### ModelSim Simulation Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/62f73d0b-7a3c-44ad-9adb-7b0baf419693)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/a7957efe-514c-4a9e-b26f-a3d97cee7ba6)

#### Quartus Prime Synthesis Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/595ec8e7-587d-411f-81e2-f65516f1b6a9)

#### Design and Testbench for 4:1 Mux in Verilog

#### Model-1 : 4:1 Mux Dataflow modelling

#### Verilog code
```
module mux_4_1_d1(I,S,Y);
	input [3:0]I;
	input [1:0]S;
	output Y;
	
    assign Y = (S==2'd0) ? I[0] : ((S==2'd1) ? I[1] : ((S==2'd2) ? I[2] : I[3])) ;

endmodule 
```

#### Testbench code
```
module mux_4_1_d1tb;
	reg [3:0]I;
	reg [1:0]S;
	wire Y;
	integer i;
	
	mux_4_1_d1 DUT(I,S,Y);
	
	initial 
		begin
			for(i=0;i<64;i=i+1)
				begin
					{I,S} = i;
					#10;
				end
		end
		
	initial 
		$monitor("time=%d, I=%b, S=%b, Y=%b", $time,I,S,Y);
	
	initial #640 $finish;
	
endmodule
```

#### ModelSim Simulation Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/add9a4d7-08c0-4618-a86d-e3c752966a1e)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/5fefaf92-e5ef-46d2-bbc9-7a35cd03dda3)

#### Quartusprime Synthesis 

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/5adab7d1-38bc-4ada-b7e7-b1e6f02ed09e)

#### Model-2 : 4:1 Mux Dataflow modelling

#### Verilog code
```
module mux_4_1_d2(I,S,Y);
	input [3:0]I;
	input [1:0]S;
	output Y;
	
    assign Y = I[S] ;

endmodule 
```

#### Testbench code
```
module mux_4_1_d2tb;
	reg [3:0]I;
	reg [1:0]S;
	wire Y;
	integer i;
	
	mux_4_1_d2 DUT(I,S,Y);
	
	initial 
		begin
			i=0;
			while(i<64)
				begin
					{I,S} = i;
					#10;
					i=i+1;
				end
		end
		
	initial 
		$monitor("time=%d, I=%b, S=%b, Y=%b", $time,I,S,Y);
	
	initial #640 $finish;
	
endmodule
```

#### ModelSim Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/5da1416c-5335-4da5-b2fb-c687d1ebe9c2)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/f6b3bc8c-6623-4140-b5a3-f0bcf0847e88)

#### QurtusPrime Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/0d9f9ddd-93d8-4b2d-be14-ee0a52c2f855)

#### Model-3 : 4:1 Mux Behavioral modelling

#### Verilog code
```
module mux_4_1_b(I,S,Y);
	input [3:0]I;
	input [1:0]S;
	output reg Y;
	
	always@(*)
		begin
			case(S)
				2'd0 : Y=I[0];
				2'd1 : Y=I[1];
				2'd2 : Y=I[2];
				2'd3 : Y=I[3];
			    default : $display("error");
			endcase
		end

endmodule
```

#### Testbench code
```
module mux_4_1_btb;
	reg [3:0]I;
	reg [1:0]S;
	wire Y;
	integer i;
	
	mux_4_1_b DUT(I,S,Y);
	
	initial 
		begin
			for(i=0;i<64;i=i+1)
				begin
					{I,S} = i;
					#10;
				end
		end
		
	initial 
		$monitor("time=%d, I=%b, S=%b, Y=%b", $time,I,S,Y);
	
	initial #640 $finish;
	
endmodule
```

#### ModelSim Simulation

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/f587539a-5133-4d2f-9df1-a8e31a8c2986)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/88c06a27-1f05-4dc6-9cce-ff93cbd066a1)

#### QuartusPrime Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/655d30bb-fb68-4cef-9706-a1ffc899271b)

#### Model-4 : 4:1 Mux Behavioral modelling

#### Verilog code
```
module mux_4_1_b1(I,S,Y);
	input [3:0] I;
	input [1:0] S;
	output reg Y;
	
	always@(*)
		begin
			if(S==2'd3)
				Y=I[3];
			else if(S==2'd2)
				Y=I[2];
			else if(S==2'd1)
				Y=I[1];
			else if(S==2'd0)
				Y=I[0];
			else $display("error");
		end
		
endmodule
```

#### Testbench code
```
module mux_4_1_b1tb;
	reg [3:0]I;
	reg [1:0]S;
	wire Y;
	integer i;
	
	mux_4_1_b1 DUT(I,S,Y);
	
	initial 
		begin
			i=0;
			while(i<64)
				begin
					{I,S} = i;
					#10;
					i=i+1;
				end
		end
		
	initial 
		$monitor("time=%d, I=%b, S=%b, Y=%b", $time,I,S,Y);
	
	initial #640 $finish;
	
endmodule
```

#### ModelSim Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/e6e68dd2-bb3f-4c6a-a145-9b52ce67ce04)

#### QuartusPrime Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/6117c9e2-7f82-43d8-b1e2-6b5a7ac4f720)

### Design and Testbench 2×4 Decoder in Verilog

#### Model-1 2x4 Decoder dataflow model

#### Verilog code
```
module decoder_2x4_d(EN,D,Y);
	input EN;
	input [1:0] D;
	output [3:0] Y;
	
	assign Y[0] = EN & ~D[1] & ~D[0];
	assign Y[1] = EN & ~D[1] & D[0];
	assign Y[2] = EN & D[1] & ~D[0];
	assign Y[3] = EN & D[1] & D[0];

endmodule
```

#### Testbench code
```
module decoder_2x4_dtb;

	reg EN;
	reg [1:0] D;
	wire [3:0] Y;
	integer i;
	
	decoder_2x4_d DUT (EN,D,Y);
	
	initial 
		begin
			for(i=0;i<8;i=i+1)
				begin	
					{EN,D} = i;
				    #10;
				end
		end
	
	initial $monitor("time=%d, enable=%b, input=%b, output=%b",$time,EN,D,Y);
	
	initial #80 $finish;
	
endmodule
```

#### ModelSim Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/422315e9-98d2-4340-8b63-3876fe0ede17)

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/df7ded23-7c70-45be-b8fa-f4b0177251a0)

#### Quartusprime Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/40c1c2fd-1702-400a-918e-e2e7779ea0b7)

#### Model-2 2x4 Decoder behavioral model

#### Verilog Code
```
module decoder_2x4_b1(EN,D,Y);
	input EN;
	input [1:0] D;
	output reg [3:0] Y;
	
	always@(*)
		begin
			if(EN)
				begin
					if(D==2'b00)
						Y=4'b0001;
					else if(D==2'b01)
						Y=4'b0010;
					else if(D==2'b10)
						Y=4'b0100;
					else if(D==2'b11)
						Y=4'b1000;
					else $display("error");
				end
			else 
			    begin
				Y=4'b0000;
				$display("enable not high");
				end
		end

endmodule
```

#### Testbench code
```
module decoder_2x4_b1tb;

	reg EN;
	reg [1:0] D;
	wire [3:0] Y;
	integer i;
	
	decoder_2x4_b1 DUT (EN,D,Y);
	
	initial 
		begin
			i=0;
			while(i<8)
				begin	
					{EN,D} = i;
				    #10;
					i=i+1;
				end
		end
	
	initial $monitor("time=%d, enable=%b, input=%b, output=%b",$time,EN,D,Y);
	
	initial #80 $finish;
	
endmodule
```

#### ModelSim Simulation

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/a051efb7-5f07-4cd9-a0c1-4df4080999f1)

#### QuartusPrime Result

![image](https://github.com/gsaisuresh/Verilog-Workshop-/assets/135144937/996181ca-4925-4689-aac7-f46eea8eab2e)








 

