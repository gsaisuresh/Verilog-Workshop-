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
    - [Verilog code which shows usage of all operators with $display and $monitor statements]
    - [Create a verilog task for conversion of Celsius into Fahrenheit]

2. [Day-02 Labs](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#day-02-lab)
    - [Dataflow based Design and Testbench for 4 bit full adder in Verilog](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#dataflow-based-design-and-testbench-for-4-bit-full-adder-in-verilog)
    - [Design and Testbench for 2:1 Mux in Verilog](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#design-and-testbench-for-21-mux-in-verilog)
    - [Design and Testbench for 4:1 Mux in Verilog](https://github.com/gsaisuresh/Verilog-Workshop-/blob/main/README.md#design-and-testbench-for-41-mux-in-verilog)
    - [Design and Testbench 2×4 Decoder in Verilog]
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


