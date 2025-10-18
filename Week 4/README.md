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


# 
# 


