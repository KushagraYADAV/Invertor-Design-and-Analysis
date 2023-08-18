# Invertor-Design-and-Analysis

In this project I'll be working with design of an inverter and understanding all the parameters involved with it. The design will utilise the models that are present under the skywater 130nm pdk and various open source tools such as, Xschem, NGSPICE, etc.

first we do the analysis of NMOS and PMOS devices, specifically the 1.8v standard models available inside the pdk. After this we start with the design of a CMOS inverter that includes schematic, measurement of various parameters like noise margin, risetime, falltime, power etc. 

For the design and simulation of our Inverter we'll use Xschem for Schematic Capture and Ngspice for Spice netlist simulation. 

## Analysis of MOSFET models
We start with the analysis of MOSFET models present in sky130 pdk. I will use the 1.8v transistor models. Below is the schematic I created in Xschem.

![image](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/61bcdae1-2728-428c-9de5-25c61ac78072)


The components used are:
nfet_01v8.sym - from xschem_sky130 library
vsource.sym - from xschem devices library
code_shown.sym - from xschem devices library

I used the above to plot the basic characteristic plots for an NMOS Transistor, that is Ids vs Vds and Ids vs Vgs
We can see the DC sweep on the VGS source for different values of VDS.
 ![image](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/503b26f9-0e37-4fe8-9e91-14c848902fc3)

 Similarly, when I sweep VDS source for different values of VGS, I get the below plot:
 ![image](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/63fe103a-39bb-4637-8c59-e27ac48815a2)

