# 32Bit_ALU Simulation

# Aim: 

Write a verilog code for 32 bit ALU supporting four logical and four arithmetic operations,use case statement and if statement for ALU behavioral modeling.

To Verify the Functionality using Test Bench.

# Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

## Design Information and Bock Diagram:

The ALU will take in two 32-bit values, and control line. An Arithmetic unit does the following task like addition subtraction, multiplication and logical operations. As the input is given in 32 bit we get 32 bit output. The arithmetic will show only one output at a time so a selector is necessary to select one of the operator.

![image](https://github.com/user-attachments/assets/e574788c-253f-46da-8468-298fe2844f7a)

### Fig 1 : Block Diagram of 32 Bit ALU 

## Creating a Work space :

Create a folder in your name (Note: Give folder name without any space) and Create a new sub-Directory name it as Exp3 or alu_32bit for the Design and open a terminal from the Sub-Directory.

## Creating Source Codes 

In the Terminal, type gedit <filename>.v (ex: gedit alu_32bit.v). 

A Blank Document opens up into which the following source code can be typed down. 

(Note : File name should be with HDL Extension)

## a)To Verify the Functionality using Test Bench

## Source Code – Using Case Statement :

module ALU (A,B,ALU_Sel,ALU_Out,CarryOut);

     input  [3:0] A, B,
    input  [2:0] ALU_Sel,
    output reg [3:0] ALU_Out,
    output reg CarryOut
    always @(*) begin
        case (ALU_Sel)
            3'b000: {CarryOut, ALU_Out} = A + B;
            3'b001: {CarryOut, ALU_Out} = A - B;
            3'b010: ALU_Out = A & B;
            3'b011: ALU_Out = A | B;
            3'b100: ALU_Out = A ^ B;
            3'b101: ALU_Out = ~A;
            3'b110: ALU_Out = A << 1;
            3'b111: ALU_Out = A >> 1;
            default: ALU_Out = 4'b0000;
        endcase
    end
endmodule


Use Save option or Ctrl+S to save the code or click on the save option from the top most right corner and close the text file.

## Creating Test bench:

Similarly, create your test bench using gedit <filename_tb>.v or <filename_tb>.vhdl to open a new blank document (alu_32bit_tb_case).

## Test Bench :

module ALU_tb;

    reg [3:0] A, B;
    reg [2:0] ALU_Sel;
    wire [3:0] ALU_Out;
    wire CarryOut;

    ALU uut (
        .A(A),
        .B(B),
        .ALU_Sel(ALU_Sel),
        .ALU_Out(ALU_Out),
        .CarryOut(CarryOut)
    );

    initial begin
        A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b000; #10;
        A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b001; #10;
        A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b010; #10;
        A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b011; #10;
        A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b100; #10;
        A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b101; #10;
        A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b110; #10;
        A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b111; #10;
        $finish;
    end
endmodule

Use Save option or Ctrl+S to save the code or click on the save option from the top most right corner and close the text file.

## Functional Simulation: 

Invoke the cadence environment by type the below commands 

tcsh (Invokes C-Shell) 

source /cadence/install/cshrc (mention the path of the tools) 

(The path of cshrc could vary depending on the installation destination)
      
After this you can see the window like below 

### Fig 2: Invoke the Cadence Environment

![Screenshot 2025-04-22 180754](https://github.com/user-attachments/assets/7a9b1a28-3ca7-4e91-ad35-421168a7ff39)


To Launch Simulation tool 

•linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design 

or

•linux:/> nclaunch& // On subsequent calls to NCVERILOG 


It will invoke the nclaunch window for functional simulation we can compile,elaborate and simulate it using Multiple Step .

### Fig 3: Setting Multi-step simulation

Select Multiple Step and then select “Create cds.lib File” as shown in below figure 

![Screenshot 2025-04-25 173631](https://github.com/user-attachments/assets/58c73056-9afc-4da6-816f-2a4644ee1218)


Click the cds.lib file and save the file by clicking on Save option 

### Fig 4:cds.lib file Creation

Save cds.lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used. 

Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in below figure .

![Screenshot 2025-04-22 181212](https://github.com/user-attachments/assets/64b9babe-cdea-40d4-bb09-66fb4dc5f7df)

We are simulating verilog design without using any libraries 

A Click “OK” in the “nclaunch: Open Design Directory” window as shown in below figure 


### Fig 5: Selection of Don’t include any libraries

A ‘NCLaunch window’ appears as shown in figure below

![image](https://github.com/user-attachments/assets/d5202b97-ee5c-4e0e-9eaf-5f3fa733e546)


Left side you can see the HDL files. Right side of the window has worklib and snapshots directories listed. 

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation .

To perform the function simulation, the following three steps are involved Compilation, Elaboration and Simulation. 

### Fig 6: Nclaunch Window

![Screenshot 2025-04-25 173218](https://github.com/user-attachments/assets/ce510288-9881-4b22-8da2-9ebe34bcd95f)


## Step 1: Compilation:

– Process to check the correct Verilog language syntax and usage 

Inputs: Supplied are Verilog design and test bench codes 

Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file 

## 	Steps for compilation: 

1. Create work/library directory (most of the latest simulation tools creates automatically)
   
2. Map the work to library created (most of the latest simulation tools creates automatically)
   
3. Run the compile command with compile options
   
i.e Cadence IES command for compile: ncverilog +access+rwc -compile fa.v 

Left side select the file and in Tools : launch verilog compiler with current selection will get enable. Click it to compile the code 

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation 

### Fig 7: Compiled database in worklib

![Screenshot 2025-04-25 173200](https://github.com/user-attachments/assets/8a3e55a6-070f-489b-b385-23db68881dc9)

After compilation it will come under worklib you can see in right side window

Select the test bench and compile it. It will come under worklib. Under Worklib you can see the module and test-bench. 

The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical

directory paths. For this Design, you will define a library called “worklib”

#3 Step 2: Elaboration:– 

To check the port connections in hierarchical design

Inputs: Top level design / test bench Verilog codes 

Outputs: Elaborate database updated in mapped library if successful, generates report else error reported in log file 

## 	Steps for elaboration 

– Run the elaboration command with elaborate options 

1.It builds the module hierarchy

2.Binds modules to module instances 

3.Computes parameter values

4.Checks for hierarchical names conflicts

5.It also establishes net connectivity and prepares all of this for simulation

After elaboration the file will come under snapshot. Select the test bench and simulate it.

## Fig 8: Elaboration Launch Option

![Screenshot 2025-04-25 173155](https://github.com/user-attachments/assets/201ed26a-3c77-4eb2-ac1f-fc30bea92532)

## Step 3: Simulation: 

– Simulate with the given test vectors over a period of time to observe the output behaviour. 

Inputs: Compiled and Elaborated top level module name 

Outputs: Simulation log file, waveforms for debugging 

Simulation allow to dump design and test bench signals into a waveform 

Steps for simulation – Run the simulation command with simulator options

## Fig 9:Simulation Waveform Window

![Screenshot 2025-04-25 173137](https://github.com/user-attachments/assets/22918987-faae-478f-9f2b-ec0ad20e7428)


### Result

The functionality of a 32-bit ALU was successfully verified using a test bench and simulated with the nclaunch tool.














      







