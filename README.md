# Invertor-Design-and-Analysis

In this project I'll be working with design of an inverter and understanding all the parameters involved with it. The design will utilise the models that are present under the skywater 130nm pdk and various open source tools such as, Xschem, NGSPICE, etc.

first we do the analysis of NMOS and PMOS devices, specifically the 1.8v standard models available inside the pdk. After this we start with the design of a CMOS inverter that includes schematic, measurement of various parameters like noise margin, risetime, falltime, power etc. 

For the design and simulation of our Inverter we'll use Xschem for Schematic Capture and Ngspice for Spice netlist simulation. 

## Analysis of MOSFET models
We start with our analysis of MOSFET models present in sky130 pdk. I would be using the 1.8v transistor models, but you can definitely use and experiment with other ones present there. below is the schematic I created in Xschem.

![image](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/e1f5fddc-3e0d-4dfa-a9cf-a74fedc28ed6)
