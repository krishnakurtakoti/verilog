# verilog


Please see the JAN_1_19_ARRAY_MULTIPLIER.docx to view the block diagram of the array multiplier.



In verilogOutputSimpleSimulation.txt,

Here,a simulation for 4 bit adder is done and the results are written into a .txt file.The test vectors are taken from .txt file.


1.Design a simple adder(4 bit adder) in verilog in Xilinx ISE.


miAdder.v

    module miAdder()
    input [3:0] a,b;
    output [3:0] sum;
    output carry;
    assign {c,sum} = a+b;
    endmodule
    
2.Now,attach a testbench tb_miAdder.v   


    module tb_four_bit_adder1;

	// Inputs
	reg [3:0] a;
	reg [3:0] b;

	// Outputs
	wire [3:0] sum;
	wire c;

	// Instantiate the Unit Under Test (UUT)
	four_bit_adder uut (
		.a(a), 
		.b(b), 
		.sum(sum), 
		.c(c)
	);


	reg [3:0] temp_aRAM [7:0];reg [3:0] temp_bRAM [7:0];
	reg [3:0] temp_sum [7:0];
	reg temp_c [7:0];
	integer i,fid;
	
	initial begin
		// Initialize Inputs
		a = 0;
		b = 0;

		// Wait 100 ns for global reset to finish
		#100;
        
		// Add stimulus here
		$readmemb("D:\\xilinx_projects\\krishnaSimulationTestBench\\testInputs\\input1.txt",temp_aRAM);
		
		$readmemb("D:\\xilinx_projects\\krishnaSimulationTestBench\\testInputs\\input2.txt",temp_bRAM);
		begin
		fid= $fopen("D:\\xilinx_projects\\krishnaSimulationTestBench\\testInputs\\output1.txt","w");
		end		
		
		for(i = 0 ;i < 8;i = i + 1)
			begin
			#40;
			a = temp_aRAM[i];
			b = temp_bRAM[i];
			#5;
			temp_sum[i] = sum;
			//$display("%b",{c, temp_sum[i]});
			$display("carry :%b ,sum : %b,total: %b",c,temp_sum[i],{c, temp_sum[i]});
			#10;
			//$fwrite(fid,"%b \t",sum1[i]);
			$fwrite(fid,"input1: %b,input2: %b,sum :%b ,carry : %b,total: %b \n",a,b,temp_sum[i],c,{c , temp_sum[i]});
			end		
		$fclose(fid);
	end
      
    endmodule
    
*********************************************************************************

      input1.txt
    0000	1001	0010	0100	0101	0110	1111

      input2.txt
    0001	1001	0010	0100	0101	0110	1111
*********************************************************************************** 
