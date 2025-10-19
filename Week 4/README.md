# India-RISC-V-Chip-Tapeout-Week4

## CMOS Circuit Design and SPICE Simulations 


### Day 1 – MOSFET Behavior & Id vs. Vds Characteristics :

First, we want to simulate the NMOS Drain current(Id) vs Drain-to-Source Voltage(Vds) for different Gate-to-source voltages (Vgs). 

We are doing this plot to observe the linear and saturation regions of a NMOS for specific Vgs values. 

#### SPICE Netlists :


    *Model Description
    .param temp=27


    *Including sky130 library files
    .lib "sky130_fd_pr/models/sky130.lib.spice" tt


    *Netlist Description



    XM1 Vdd n1 0 0 sky130_fd_pr__nfet_01v8 w=5 l=2

    R1 n1 in 55

    Vdd vdd 0 1.8V
    Vin in 0 1.8V

    *simulation commands

    .op
    .dc Vdd 0 1.8 0.1 Vin 0 1.8 0.2

    .control

    run
    display
    setplot dc1
    .endc

    .end


To simulate this SPICE Netlist, we use *ngspice* as :

    ngspice file_name.spice
Then, to plot the drain current (Id)  :

    plot -vdd#branch

#### Plots :

![D1 nmos id vs vds](https://github.com/user-attachments/assets/1e46f7bb-29ef-4acf-8728-82d6fc7dc541)


 
  #
  #
#### Observations :
    
1] Here, we can clerly observe that for a specific value of Vgs, the current Id is first linearly increases with drain-to-source voltage (Vds), then after a specific value of Vds = Vgs- Vth,(where Vth is the threshold Voltage of the NMOS) the current Id almost saturates with Vds. 

**Explanation :** For a specific value of Vgs (>= Vth), in NMOS channel region is formed under the Gate Oxide region between the source and drain region. So, appling a +ve Vds between drain and source, electron flows through the channel region from source to drain end and so current flows through the drain to source. Now, if Vds= Vgs-Vth then the drain end depletion region increased such that it lowered the channel thickness at the drain end to almost negligible and the current then stops increasing and saturates as further Vds increases. 

2] As, we know, a NMOS is turned on when Vgs is greater or equals to the threshold voltage (Vth). Here, we can see that Id- Vds plots for Vgs value of 1.8V, 1.6V and goes on till 0.8V. Below which, we can't observe as Vgs becomes comparable to threshold voltage(Vth) value or less than that. And, if we zoom in the cutoff region (Figure below) we can see that a small current is there (just above the Vds axis) for the Vgs value of 0.6 V. 

**Explanation :** For, Vgs < Vth, the inversion channel is not formed under the gate region. So, there is no conducting direct path between the drain and source. So, no significant current flows through drain and source.

![D1 nmos id vs vds zoom](https://github.com/user-attachments/assets/35417ae3-0736-485b-a05b-c99e6feb107e)


3] The Id values at saturation changes quadratically with the Vgs values. 

**Explanation :**
The drain current(Id) in the saturation region for a Large Channel MOSFET is given by:

$$I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{GS} - V_{th})^2$$

Here, we took the Channel length of 2 micrometer. So, there is no such small channel effects. And Id changes quadritically with Vgs in saturation region as the above equation states. 
# 
# 

### Day 2 –  Threshold Voltage Extraction & Velocity Saturation  :

**PART -1 :**

First, we will do the Id vs Vds plot for a NMOS with channel length of 0.15 micrometer to observe how the MOSFET charecteristics changes with the small channel effects. 

#### SPICE Netlists :


    *Model Description
    .param temp=27


    *Including sky130 library files
    .lib "sky130_fd_pr/models/sky130.lib.spice" tt


    *Netlist Description



    XM1 Vdd n1 0 0 sky130_fd_pr__nfet_01v8 w=0.39 l=0.15

    R1 n1 in 55

    Vdd vdd 0 1.8V
    Vin in 0 1.8V

    *simulation commands

    .op
    .dc Vdd 0 1.8 0.1 Vin 0 1.8 0.2

    .control

    run
    display
    setplot dc1
    .endc

    .end



To simulate this SPICE Netlist, we use *ngspice* as :

    ngspice file_name.spice
Then, to plot the drain current (Id) :

    plot -vdd#branch

#### Plots :

![D2 id vds 2](https://github.com/user-attachments/assets/7332a838-f422-48e3-940c-cb07a19caa2c)


 
  #
  #
#### Observations :
    
Here, we can clearly observe that the current in saturation region is not constant with Vds, it's increasing linearly with Vds. 

And the current in the saturation region varries with Vgs linearly. 

**Explanation :** 
For a small Channel MOSFET with considering the velocity saturation and channel length modulation, the Drain current (Id) in saturation region is given by 
  
$$I_D =  \mu_n C_{ox} \frac{W}{L} V_{DSAT} [(V_{GS} - V_T) -\frac{1}{2} V_{DSAT}] \cdot (1 + \lambda V_{DS})$$


From this above equation we can clearly see that the drain current is linearly changes with Vds. And the current Id is a linear function of Vgs, so the current in the saturation region varries with Vgs linearly. 

 

# 
# 

**PART -2 : Id vs Vgs**

Here, we will do the Id vs Vgs plot of a NMOS for a fixed value of Vds, to extract the Threshold Voltage(Vth) value of the NMOS. 


#### SPICE Netlists :


    *Model Description
    .param temp=27


    *Including sky130 library files
    .lib "sky130_fd_pr/models/sky130.lib.spice" tt


    *Netlist Description

    XM1 Vdd n1 0 0 sky130_fd_pr__nfet_01v8 w=0.39 l=0.15

    R1 n1 in 55

    Vdd vdd 0 1.8V
    Vin in 0 1.8V

    *simulation commands

    .op
    .dc Vin 0 1.8 0.1 

    .control

    run
    display
    setplot dc1
    .endc

    .end



To simulate this SPICE Netlist, we use *ngspice* as :

    ngspice file_name.spice
Then, to plot the drain current (Id) :

    plot -vdd#branch

#### Plots :

![D2 id vgs 2](https://github.com/user-attachments/assets/6cacbd3a-e040-4bf0-a119-5aa9fa54537f)

# 
![D2 id vgs vth x0 = 0 778049](https://github.com/user-attachments/assets/1591b3e5-70e5-4df2-96ee-2dd672b6c282)

 
  #
  #
#### Results :
    
By, linear extrapolation, we got the Threshold Voltage value as :

**Threshold Voltage (Vth) = 0.778049 V**

 (In the above zoom in figure, the Vth point is marked in the Vgs axis)

# 
# 


### Day 3 –  CMOS Inverter: Voltage Transfer Characteristic (VTC) and Transient Behavior (Rise/Fall Delays)   
**PART -1 : Switching Threshold Voltage**

Here, we will plot the Voltage Transfer Characteristic (VTC) of a CMOS inverter with specification :

PMOS : Width (W)= 0.84 micron , Length (L)= 0.15 micron

NMOS : Width (W)= 0.36 micron, Length (L)= 0.15 micron


#### SPICE Netlists :


    *Model Description
    .param temp=27


    *Including sky130 library files
    .lib "sky130_fd_pr/models/sky130.lib.spice" tt


    *Netlist Description


    XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.15
    XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15


    Cload out 0 50fF

    Vdd vdd 0 1.8V
    Vin in 0 1.8V

    *simulation commands

    .op

    .dc Vin 0 1.8 0.01

    .control
    run
    setplot dc1
    display
    .endc

    .end



To simulate this SPICE Netlist, we use *ngspice* as :

    ngspice file_name.spice
Then, to plot the VTC of the CMOS Inverter :

    plot out vs in

#### Plots :

![D3 vtc 2](https://github.com/user-attachments/assets/fb36e374-c5e5-403c-80dd-b2e7507185aa)

# 

![D3 vtc swt th](https://github.com/user-attachments/assets/dfb9a5c8-b80f-41b9-818f-438f0b41cd66)


 
  #
  #
#### Results :
    
From the VTC plot of the CMOS Inverter, extracted the Switching Threshold Voltage at the point on VTC where the Vin = Vout. 

In the above zoomed figure, at the marked point, **Vin= 0.876905 V** and **Vout= 0.876914 V** 

**Switching Threshold Voltage (Vm) = 0.8769 V**

 

# 
# 

**PART -2 :Transient Behavior (Rise/Fall Delays) of CMOS Inverter**

Here, we will do the Transient Analysis of a CMOS Inverter and from the plot will calculate the rise and fall Propagation Delays.

#### SPICE Netlists :


    *Model Description
    .param temp=27


    *Including sky130 library files
    .lib "sky130_fd_pr/models/sky130.lib.spice" tt


    *Netlist Description


    XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.15
    XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15


    Cload out 0 50fF

    Vdd vdd 0 1.8V
    Vin in 0 PULSE(0V 1.8V 0 0.1ns 0.1ns 2ns 4ns)

    *simulation commands

    .tran 1n 10n

    .control
    run
    .endc

    .end




To simulate this SPICE Netlist, we use *ngspice* as :

    ngspice file_name.spice
Then, to plot the Transient Behavior of the CMOS Inverter :

    plot out vs time in

#### Plots :


![D3 tran 2 ](https://github.com/user-attachments/assets/6f47cef2-e3ff-49be-ad73-2bf8ac064d39)


 
  #
  #

  **For Rise Delay Calculations :**


![D3 tran rise a = 2 48289e-09, b = 2 14934e-09](https://github.com/user-attachments/assets/0efe222f-0399-4c8d-afee-8dbbaac8967d)


  Here, zoomed in where the Vout is rising and marked the points 'a' and 'b' on Vout and Vin respectively at Vdd/2 (Here, Vdd=1.8V so, at 0.9V) 

Now, the time axis at the points :
a= 2.48289 ns and b= 2.14934 ns

  So, the Rise Delay = 0.33355 ns


 #
  #

  **For Fall Delay Calculations :**
  

![D3 tran fall a = 4 33409e-09, b = 4 04943e-09](https://github.com/user-attachments/assets/9ef7d09f-5c7a-42ca-871e-f575c593927d)



 Here, zoomed in where the Vout is failing and marked the points 'a' and 'b' on Vout and Vin respectively at Vdd/2 (Here, Vdd=1.8V so, at 0.9V) 

Now, the time axis at the points :
a= 4.33409 ns and b= 4.04943 ns

  So, the Fall Delay = 0.28466 ns
#
  #

#### Results :
    

**Rise Propagation Delay(t_rise) = 0.33355 ns**

**Fall Propagation Delay(t_fall) = 0.28466 ns**

 

# 
# 
### Day 4 –  CMOS Inverter: Noise Margin / Robustness Analysis 


First, we will plot the Voltage Transfer Characteristic (VTC) of a CMOS inverter with specification :

PMOS : Width (W)= 1 micron , Length (L)= 0.15 micron

NMOS : Width (W)= 0.36 micron, Length (L)= 0.15 micron

Then from the VTC plot, we will calculate the Noise Margins of the CMOS Inverter.

#### SPICE Netlists :


    *Model Description
    .param temp=27


    *Including sky130 library files
    .lib "sky130_fd_pr/models/sky130.lib.spice" tt


    *Netlist Description


    XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=1 l=0.15
    XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15


    Cload out 0 50fF

    Vdd vdd 0 1.8V
    Vin in 0 1.8V

    *simulation commands

    .op

    .dc Vin 0 1.8 0.01

    .control
    run
    setplot dc1
    display
    .endc

    .end




To simulate this SPICE Netlist, we use *ngspice* as :

    ngspice file_name.spice
Then, to plot the VTC of the CMOS Inverter :

    plot out vs in

#### Plots :


![D4 NM vil=0 762766, voh = 1 72364, vih= 1 00851, vol= 0 0763636](https://github.com/user-attachments/assets/b045910a-98ea-42e3-9bdd-4d3aec3c414f)



 
  #
  #

 

#### Results :
    
Now, on the VTC plot pointed out the points 'A' and 'B' where the slop of the curve, i.e. dVout/ dVin = -1.


At point 'A', Vin= 0.762766 and Vout= 1.72364

At point 'B', Vin= 1.00851 and Vout= 0.0763636

**So, V_IL=0.762766    and   V_OH= 1.72364**

**V_IH= 1.00851 and V_OL= 0.0763636**

 **Noise Margin High (NM_H) = V_OH - V_IH = 0.71513 V**

 **Noise Margin Low (NM_L) = V_IL - V_OL = 0.6864 V**
# 
# 


### Day 5 –  CMOS Inverter Robustness

### PART 1 : Power Supply Variation

Here, we want to varry the supply voltage of the CMOS Inverter and we will observe the corresponding VTC of the inverter, change in Switching Threshold Voltage (Vm) and Gain as the supply voltage changes.

Here, we took a CMOS inverter with specification :

PMOS : Width (W)= 1 micron , Length (L)= 0.15 micron

NMOS : Width (W)= 0.36 micron, Length (L)= 0.15 micron

Then from the plot, we will calculate the Switching Threshold Voltage (Vm) and Gain for specific supply voltages.

#### SPICE Netlists :


    *Model Description
    .param temp=27


    *Including sky130 library files
    .lib "sky130_fd_pr/models/sky130.lib.spice" tt


    *Netlist Description


    XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=1 l=0.15
    XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15


    Cload out 0 50fF

    Vdd vdd 0 1.8V
    Vin in 0 1.8V

    .control

    let powersupply = 1.8
    alter Vdd = powersupply
	let voltagesupplyvariation = 0
	dowhile voltagesupplyvariation < 6
	dc Vin 0 1.8 0.01
	let powersupply = powersupply - 0.2
	alter Vdd = powersupply
	let voltagesupplyvariation = voltagesupplyvariation + 1
    end
 
    plot dc1.out vs in dc2.out vs in dc3.out vs in dc4.out vs in dc5.out vs in dc6.out vs in xlabel "input voltage(V)" ylabel "output voltage(V)" title "Inveter dc characteristics as a function of supply voltage"

    .endc

    .end





To simulate this SPICE Netlist, we use *ngspice* as :

    ngspice file_name.spice

#### Plots :


![D5 supply 2 vtc](https://github.com/user-attachments/assets/646f3c00-7d67-46b2-8e13-9c4c3f0f3b75)


 
  #
  #

**To Find out the Switching Threshold for different Supply Voltages :**

I additionally plot a straight line for "Vout=Vin" to easily find out the Switching Threshold points on each VTC curve for different supply voltages. 

In this below figure, I marked all the Switching Threshold points on each VTC curve.

# 

![D5 supply final Vm](https://github.com/user-attachments/assets/92d4e52e-d02e-4a74-9852-d8a12d856166)



# 

**To Find out the Gain of the Inverter for different Supply Voltages :**

In the below figure, I marked the points where dVout/dVin = -1, and from the (Vin,Vout) values at those points on each VTC, we calculated the corresponding gain of the Inverter. 


# 

![D5 supply final gain](https://github.com/user-attachments/assets/7c2d7534-4b23-412c-8c03-cf7daae2bcc8)



# 
# 

#### Results :
    
The Switching Threshold Voltage and Gain for different supply voltages are tabulated in the below table.




| Supply Voltage | Switching Threshold Voltage (Vm) | Gain |
| :--- | :--- | :--- | 
| 1.8 V | 0.88 | 7.23 | 
| 1.6 V | 0.793 | 8.594 | 
| 1.4 V | 0.698 | 9.453 | 
| 1.2 V | 0.611 | 9.96 | 
| 1.0 V | 0.533 | 10.125 | 
| 0.8 V | 0.456 | 9.72 | 


# 
# 

### PART 2 : Device Variation

Here, we want to varry the PMOS and NMOS width of the CMOS Inverter and we will observe the corresponding VTC of the inverter, change in Switching Threshold Voltage (Vm) and Noise Margin as the Wp/Wn width ratio changes.

Initially, we took a CMOS inverter with specification :

PMOS : Width (Wp)= 7 micron , Length (L)= 0.15 micron

NMOS : Width (Wn)= 0.42 micron, Length (L)= 0.15 micron

Next, we will change the Wp and Wn subsequently whereas we fixed the channel length of both the NMOS and PMOS to 0.15 micron.

Then from the plot, we will calculate the Switching Threshold Voltage (Vm) and Noise Margin for specific devices.

#### SPICE Netlists :


    *Model Description
    .param temp=27


    *Including sky130 library files
    .lib "sky130_fd_pr/models/sky130.lib.spice" tt


    *Netlist Description


    XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=7 l=0.15
    XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.42 l=0.15


    Cload out 0 50fF

    Vdd vdd 0 1.8V
    Vin in 0 1.8V

    *simulation commands

    .op

    .dc Vin 0 1.8 0.01

    .control
    run
    setplot dc1
    display
    .endc

    .end







To simulate this SPICE Netlist, we use *ngspice* as :

    ngspice file_name.spice

Then to plot the VTC :

    plot out vs in
#### Plots :

# 

**Case 1 : Wp=7 micron and Wn= 0.42 micron**

![D5 device c1 wp 7 wn 0 42](https://github.com/user-attachments/assets/2d7dbcfd-fe79-4381-ac1c-bfb2384ace17)



# 

**Case 2 : Wp=5 micron and Wn= 0.55 micron**


![D5 device c2 wp 5 wn 0 55](https://github.com/user-attachments/assets/57262e94-b4a7-4bf4-ad5f-e87ff83d6497)


# 


**Case 3 : Wp=3 micron and Wn= 0.64 micron**


![D5 device c3 wp 3 wn 0 64](https://github.com/user-attachments/assets/f734be61-c34a-41c5-95d3-48baa6450b1c)


# 


**Case 4 : Wp=2 micron and Wn= 0.84 micron**


![D5 device c4 wp 2 wn 0 84](https://github.com/user-attachments/assets/21ef49e9-c6bc-4a25-bc28-766c885ca638)


# 


**Case 5 : Wp=1 micron and Wn=1 micron**


![D5 device c5 wp 1 wn 1](https://github.com/user-attachments/assets/18572cd7-2ce8-42a2-b347-31aafe109c39)


# 


**Case 6 : Wp=0.84 micron and Wn=2 micron**


![D5 device c6 wp 0 84 wn 2](https://github.com/user-attachments/assets/a53d16da-161a-4dc3-8501-f4e25995d6d0)


# 


# 
# 

#### Results :
    
The Switching Threshold Voltage and Noise Margins for different Wp/Wn ratios are tabulated in the below table.




| Width of PMOS (Wp) | Width of NMOS (Wn) | Wp/Wn Ratio | Switching Threshold Voltage (Vm) | Noise Margin Low (NM_L) | Noise Margin High (NM_H) |
| :--- | :--- | :--- | :--- |:--- |:--- | 
| 7 μm | 0.42 μm | 16.67 | 0.989 | 0.8225 | 0.5831 |
| 5 μm | 0.55 μm | 9.09 | 0.9536 | 0.7881 | 0.6164 |
| 3 μm | 0.64 μm | 4.68 | 0.922 | 0.7408 | 0.6724 |
| 2 μm | 0.84 μm | 2.38 | 0.878 | 0.7014 | 0.7168 |
| 1 μm | 1 μm | 1 | 0.834 | 0.6501 | 0.7971 |
| 0.84 μm | 2 μm | 0.42 | 0.781 | 0.5721 | 0.8927 |


# 
# 

#### Observations :

As, the Wp/Wn ratio starts decreasing, i.e., PMOS is getting weaker and NMOS is getting stronger than the previous case, the corresponding Switching Threshold Voltage moves to the left and the Noise Margin (Low) decreases whereas the Noise Margin (High) increases as the Wp/Wn ratio decreases. 

# 
# 


