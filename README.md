# 1 Invertor-Design-and-Analysis

In this project, I'll be working on the design of an inverter and understanding all the parameters involved with it. The design will utilize the models that are present under the skywater 130nm pdk and various open-source tools such as Xschem, NGSPICE, etc.

First, we do the analysis of NMOS and PMOS devices, specifically the 1.8v standard models available inside the pdk. After this, we start with the design of a CMOS inverter that includes a schematic, and measurement of various parameters like noise margin, rise time, fall time, power, etc. 

For the design and simulation of our Inverter, we'll use Xschem for Schematic Capture and Ngspice for Spice Netlist simulation. 

## 1.1 Analysis of MOSFET models
We start with the analysis of MOSFET models present in sky130 pdk. I will use the 1.8v transistor models. Below is the schematic I created in Xschem.

![image](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/484f4e57-b0d7-40ae-a4d7-0a9c8fe1f821)



The components used are:
nfet_01v8.sym - from xschem_sky130 library
vsource.sym - from xschem devices library
code_shown.sym - from xschem devices library

I used the above to plot the basic characteristic plots for an NMOS Transistor, that is, Ids vs Vds and Ids vs Vgs
We can see the DC sweep on the VGS source for different values of VDS:

![Screenshot from 2023-08-16 15-31-23](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/3bed2355-5887-4dee-a8a7-a4c7e06a84ee)

Similarly, when we sweep the VDS source for different values of VGS, I get the below plot:

![Screenshot from 2023-08-16 15-23-02](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/caf5a8d2-ae7b-4e48-be29-2af806ab256b)

## 1.2 CMOS Inverter Design and Analysis
I have designed a Schematic of the Inverter, where the Width ratio of PMOS to NMOS is 2,two and a pulse is applied as input. The schematic is shown below: The transfer characteristics is given below:

![Screenshot from 2023-08-19 14-27-56](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/a8ed229b-75f9-4811-bfb7-47c5256ebb71)

 
And the transfer characteristics for the transient analysis is given below:

![Screenshot from 2023-08-19 14-27-15](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/d5238a9c-a951-4535-bd0f-32a1bff1e24a)


Now we want to find the switching threshold at which vin=vout. For this, we need to do the dc analysis of the CMOS inverter. We can convert our inverter into an equivalent symbol as shown below: 

![Screenshot from 2023-08-17 13-51-35](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/b4a3f545-cf75-4480-a961-53733e1836b3)

The Plot of Vout vs Vin is shown below:

![Screenshot from 2023-08-17 14-08-07](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/9b803f96-875e-4a45-b27b-4cd1b54c581d)

We can also find lower and higher noise margins. For that, we know that

VOH - Maximum output voltage when it is logic '1'.   
VOL - Minimum output voltage when it is logic '0'.   
VIH - Maximum input voltage that can be interpreted as logic '0'.  
VIL - Minimum input voltage that can be interpreted as logic '1'.  

The noise margins are given as:    
NML(Noise Margin for Low) = VIL - VOL      
NMH(Noise Margin for HIGH) - VOH - VIH     

We can now find the trip point Vm and also the Noise Margins by using the below codes:

![Screenshot from 2023-08-19 14-53-16](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/f1073a36-8b22-4d6b-940e-6c0873a1d121)

NML=VIL-VOL  
   =0.7435-0  
   =0.7435   

NMH=VOH-VIH   
   =1.8-0.98   
   =0.82    

The values of VOH and VOL are not exactly 1.8 and 0 respectively, but are somewhat less than 1.8V and greater oV respectively.    

The plot of gain, vout vs vin is shown below:

![Screenshot from 2023-08-19 15-01-46](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/e40a2160-7890-4c51-8912-b9b6e52da066)


Now we move forward to calculate propagation delay, rise time and fall time. For this we again move to the transient analysis. 

The schematic as shown below:  

![Screenshot from 2023-08-17 13-53-15](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/b7f202d5-4d3e-46cd-95a5-9f2105ef6cc7)


We write the following code to find the 50% threshold of vin and vout and then calculate the propagation delay:

![Screenshot from 2023-08-19 16-13-49](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/2f58af8f-c673-4324-8d29-bf1be83792fc)

We take the average of tpLH and tpHL to find the overall propagation delay.    

Note that all the measurements are done without considering a load capacitance at the output of the inverter.    
Now we will calculate the rise time of the CMOS inverter. We use the following code to do that:   

![Screenshot from 2023-08-19 16-20-22](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/b81af859-7d31-4b3c-bbc9-b45af1651e1d)

Vout, vin curve with respect to time is shown below:   
![Screenshot from 2023-08-17 14-43-29](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/fea59d97-342f-4bfc-920a-cc4dc648976a)


Now we consider a load capacitance at the output of our invertor. The value of the capacitance we consider is 0.5pF. The schematic is shown below: 

![Screenshot from 2023-08-17 13-53-15](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/c30feaf9-fb80-4858-893b-0797fd3c4ab7)


Note that, for unloaded invertors, doubling the sizes of the NMOS and PMOS doesn't have much effect on rise time. For loaded invertor, it will have effect. We will look into how much effect that 
will have by taking the Widths to be 2,1 the first case and 4,2 the second case.

For the width of Pmos and NMOS to be 2 and 1 respectively, the rise time in presence of a load can be calculated as: 

![Screenshot from 2023-08-19 16-27-15](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/ebf5433a-7793-416e-aff5-c7463b64746e)

Vout, vin curve with respect to time is shown below:   

![Screenshot 2 1  1 8](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/8f758dd4-5437-4389-956c-574ce147c4e3)


For the width of PMOS and NMOS to be 4 and 2, respectively, the rise time in the presence of a load can be calculated as follows: 

![Screenshot from 2023-08-19 16-29-13](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/059e094b-cd04-4940-9b21-fafea664263f)


Vout, vin curve with respect to time is shown below:  

![Screenshot 4 1 1 8](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/7e9b5c5c-0f71-4641-bcae-dc7782f3f90f)


We can see there is a significant drop in the rise time by doubling the widths of NMOS and PMOS. Also, the rise time in the 0.5pF case is more compared to 02pF, as 0.5pF has more charging time
than 0.2pF.

Now we move forward to calculate power in both cases when the load is 0.5pF and when it is 0.2pF. These values will be calculated for widths of PMOS and NMOS as 4 and 2 respectively. 
For 0.5pf case, it is given as : 

![Screenshot from 2023-08-19 16-58-26](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/6056ab27-8467-458f-973b-f709cde235e5)


For 0.2pf case, it is given as : 

![Screenshot from 2023-08-19 17-00-03](https://github.com/KushagraYADAV/Invertor-Design-and-Analysis/assets/65351472/3b07b30c-29b1-4aec-8ab3-d4f4a300fb14)

We can infer that power is more in the case of 0.5pF case as it draws more current while charging. 























 

