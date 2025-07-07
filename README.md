# VSD-TCL-Workshop

This repository contains my learnings from the TCL programming workshop conducted by VLSI System Design.

The aim of the workshop is to write a TCL script that processes the synthesis collaterals of a design and gives us the prelayout timing results as output.

DAY1

Below is the csv file that contains the path to the input files needed for synthesis

![Screenshot (808)](https://github.com/user-attachments/assets/fbabf856-8bbd-4a30-9474-34ccfd0768c8)

Using the csv file as arg, the shell script to invoke the TCL script:

![Screenshot (807)](https://github.com/user-attachments/assets/cc78cc4f-6612-4e6f-a085-fddc7ceda121)

DAY2

TCL code to extract the list of input variables from csv:

![Screenshot (809)](https://github.com/user-attachments/assets/820924be-6cef-4f33-beac-b2cd2349c4d9)

Checks to see if the paths mentioned in csv are present:

![Screenshot (810)](https://github.com/user-attachments/assets/6d7d9778-acb3-47de-93a2-5421cd90384e)

We need to convert the constraints file into sdc format (Synopsys Design Constraints)

From   
                                        ![Screenshot (813)](https://github.com/user-attachments/assets/146d0dd7-3d50-4cc7-bacf-abafb9d41c26)
To
                                        ![Screenshot (814)](https://github.com/user-attachments/assets/acc9e19f-a6b4-4c0d-8afe-81f4431682e8)

Formatting clock constraints:

![Screenshot (811)](https://github.com/user-attachments/assets/dad87765-02ed-445e-8876-74453b7f20ce)

Formatting input constraints:
It is important to identify bussed IO ports with suffix "*" in the sdc file 
![Screenshot (812)](https://github.com/user-attachments/assets/a743049b-e1c4-4d53-ab45-9d3e457135b8)

 ![Screenshot (818)](https://github.com/user-attachments/assets/dbced72d-2380-4f8b-aa70-0d70ec8b8f03)

Similarly, formatting output constraints:

![Screenshot (819)](https://github.com/user-attachments/assets/5193a9bd-7bec-439f-a11f-0075dc42d035)

![Screenshot (820)](https://github.com/user-attachments/assets/e4ec68d6-1b95-462a-aac6-7d4f92e658b9)

We then create a hierarchy check script to be used by Yosys to verify that all RTL modules referenced in the Top module are defined properly and available for synthesis

TCL code to make hierarchy check script:

![Screenshot (821)](https://github.com/user-attachments/assets/f521d200-6e9b-4359-9bec-08e5b9ca4cdf)

Resulting hier.ys 

![Screenshot (822)](https://github.com/user-attachments/assets/b639345a-aed4-41b2-a100-be8ca60563c4)

Hierarchy pass in yosys hierarchy check log:

![Screenshot (823)](https://github.com/user-attachments/assets/940cc5c2-27e4-4726-8946-c4f44cd62763)

DAY 5

Now, we make the main synthesis script script to be executed in Yosys:

![Screenshot (824)](https://github.com/user-attachments/assets/e9b58a60-82b3-44c8-bd18-73b5c611afb6)

Resulting ys file:

![Screenshot (825)](https://github.com/user-attachments/assets/89f17baf-dc5d-4da0-8550-e99445ec5be9)


Upon executing this script in Yosys tool, the tool performs synthesis and write out a verilog netlist

![Screenshot (826)](https://github.com/user-attachments/assets/d50e11cd-e438-4af4-b5bb-375b1c8a4d64)

We need to perform Static Timing Analysis on this netlist using the OpenTimer tool. 
So we replace the "\\" characters from the Yosys generated synthesis netlist with empty string "" to make it compatible with OpenTimer.

![Screenshot (824)](https://github.com/user-attachments/assets/a181253b-8f86-4a66-bdb6-61947f43a82c)


Now, it's time for Static Timing Analysis

![Screenshot (832)](https://github.com/user-attachments/assets/b48790db-ff19-4d52-b769-a7ea955de130)


We change the output log from Stdout to conf file using proc reOpenStdout.proc

set multi cpu usage with desired number of thread using set_num_threads.proc
![Screenshot (833)](https://github.com/user-attachments/assets/cfdf819c-cac5-44f2-ab83-91837eeaa408)


set early cell library, late cell library path using read_lib.proc

set verilog path (final synthesis netlist to be read into OpenTimer) using read_verilog.proc

Using read_sdc.proc we convert the sdc file we ceated earlier into timing file readable by OpenTimer. This proc extracts the port name, clock period, duty cycle, input and output delays. It converts the bussed ports into bit blasted ports

From
![Screenshot (830)](https://github.com/user-attachments/assets/0a61a166-7114-4b86-9ed4-af8733490d11)

To
![Screenshot (831)](https://github.com/user-attachments/assets/64e7d14a-64f5-440c-8ebe-740f1df505ff)








