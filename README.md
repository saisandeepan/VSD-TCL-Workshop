# VSD-TCL-Workshop

This repository contains my learnings from the TCL programming workshop conducted by VLSI System Design.

The aim of the workshop is to create a TCL script that processes the synthesis collaterals of a design and gives us the prelayout timing results as output.

DAY1

Below is the csv file that contains the paths to the input files needed for synthesis

![Screenshot (808)](https://github.com/user-attachments/assets/fbabf856-8bbd-4a30-9474-34ccfd0768c8)

Using the csv file as arg, the shell script to invoke the TCL script:

![Screenshot (807)](https://github.com/user-attachments/assets/cc78cc4f-6612-4e6f-a085-fddc7ceda121)

DAY2

TCL code to extract the list of input variables from csv:

![Screenshot (809)](https://github.com/user-attachments/assets/820924be-6cef-4f33-beac-b2cd2349c4d9)

Checks to see if files are present in the paths mentioned in csv:

![Screenshot (810)](https://github.com/user-attachments/assets/6d7d9778-acb3-47de-93a2-5421cd90384e)

We need to convert the constraints file into sdc format understadable by Yosys tool
                                        From   
                                        ![Screenshot (813)](https://github.com/user-attachments/assets/146d0dd7-3d50-4cc7-bacf-abafb9d41c26)
                                        to
                                        ![Screenshot (814)](https://github.com/user-attachments/assets/acc9e19f-a6b4-4c0d-8afe-81f4431682e8)

Formatting the clock constraints:

![Screenshot (811)](https://github.com/user-attachments/assets/dad87765-02ed-445e-8876-74453b7f20ce)

Formatting input constraints:


