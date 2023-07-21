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
    - [Structural Design and Testbench for one bit full adder in Verilog using HalfAdder]
    - [Verilog code which shows usage of all operators with $display and $monitor statements]
    - [Create a verilog task for conversion of Celsius into Fahrenheit]

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
