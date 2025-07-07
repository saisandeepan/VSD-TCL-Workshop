# VSD-TCL-Workshop

This repository contains my learnings from the TCL programming workshop conducted by VLSI System Design.

The aim of the workshop is to create a TCL script that processes the synthesis collaterals of a design and gives us the prelayout timing results as output.

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

We need to convert the constraints file into sdc format understadable by the synthesis tool - Yosys

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




