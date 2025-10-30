# India-RISC-V-Chip-Tapeout-Week6

##  Physical Design Workshop 


### Day 1 : Set up the OpenLane Flow and run Synthesis 


First, we are going to set up the OpenLane environment. For that open the terminal in Ubuntu and use the commands as :

    cd Desktop/work/tools/openlane_working_dir/openlane

    docker


Now, we can invoke the OpenLANE flow in the Interactive mode as :

    ./flow.tcl -interactive

Next input the required packages

    package require openlane 0.9


![day 1 1](https://github.com/user-attachments/assets/734a4baf-2335-432f-9fd8-bdfd98e5e2d3)




Now, we will synthesize the *picorv32a* design already available in the design directory.

    prep -design picorv32a

    run_synthesis



![day 1 2](https://github.com/user-attachments/assets/12c9dbd6-04de-4ee7-a0de-1f766af01bab)




### Calculation of the Flop Ratio in *picorv32a* :

From the synthesis logs can calculate the Flop Ratio as : 
 
**Flop Ratio = (No.of d Flip-flops / Total no. of cells in design)**



**Synthesis Log :**


![day 1 3](https://github.com/user-attachments/assets/5f1e3044-bce8-4494-9ccf-30b8f321b86c)



Also, we can find the yosys synthesis log in the *../design/picorv32a/runs/reports/synthesis/* directory. we can open the reports with *gvim* command.

**Yosys statistics report :**




![day 1 5 yosys](https://github.com/user-attachments/assets/8f92f13e-c359-437e-b0a1-d8f772d77c28)


# 

Now, from the above reports, we get,

No. of D Flip-flops = 1613
Total no. of cells in design = 14876

So, **Flop Ratio** = (No.of d Flip-flops / Total no. of cells in design) = **1613/14876 = 0.1084296853**

So, (in %) **Percentage of Flip-Flops = 10.84296853 %**

# 


In the *../report/synthesis/* directory we can also observe the generated Timing reports :


![day 1 6 time](https://github.com/user-attachments/assets/8b48c62c-b52e-4abd-960c-d710513cd29f)



![day 1 7 time](https://github.com/user-attachments/assets/1f711903-6088-4f61-b8a2-20c97c8dd614)


# 


In the *../results/synthesis/* directory we can find out the generated Netlist :



![day 1 4 netlist](https://github.com/user-attachments/assets/12dfffa5-cee6-4922-b5b0-54dcaabd1211)



# 
# 


### Day 2 : Floorplan and Placement

### Part -1 : Floorplan


First, we will do the floorplan of the *picorv32a* design using OpenLANE flow. To invoke the OpenLANE flow we follow as mentioned in Day 1. After the *run_synthesis* command we use the floorplan command as :


    run_floorplan



![day 2 1](https://github.com/user-attachments/assets/a8f04a96-f33c-4d52-9d7f-f70e47c7b45d)



### Calculation of the Die Area from the Floorplan Logs:

We can find the Floorplan output logs in the *../design/picorv32a/runs/date/reports/floorplan/* directory. The output logs are in the *picorv32a.floorplan.def* file.


Floorplan report :



![day 2 2](https://github.com/user-attachments/assets/a5101b36-dddc-4b2c-9113-fb33a1592ce9)






Now, from the above reports, we get,

1 Micron = 1000 Unit Distance

Die width (in Unit Distance) = 660685-0 = 660685

So, **Die width (in Microns) = 660685/1000 = 660.685 Microns**



Die height (in Unit Distance) = 671405-0 = 671405

So, **Die height (in Microns) = 671405/1000 = 671.405 Microns**



So, **Area of the Die = (660.685 * 671.405) Sq. Microns = 443587.212 Sq. Microns**.


# 

### Visualization of the Floorplan in *Magic* Tool :

To load the generated floorplan in magic tool, use this commands as :


    #first change the directory to the generated results directory ../results/floorplan/ 
    
    cd ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/30-10_10-57/results/floorplan/
    

    magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &


**Useful Note :**

Inside the magic tool, to fit the whole floorplan with our screen use **'q' and 's' key simulteneously and then press 'v'**.

**Press 'z' for Zoom In and 'Shift + z' for Zoom Out**.

**To select any cell** just move the curser onto the cell and then **press 'i'**.

# 
Screenshots of the Floorplan :



![day 2 3](https://github.com/user-attachments/assets/5f8d49ac-0162-444d-b7cf-2ae29682343f)
# 
![day 2 4](https://github.com/user-attachments/assets/e900e770-84e0-42e4-9e75-40b1cc156726)
# 
![day 2 5](https://github.com/user-attachments/assets/8fbb317d-1e7d-459e-82bc-7bae6205f31f)
# 
![day 2 6](https://github.com/user-attachments/assets/b0c48aa3-76f8-4aeb-a88a-8d906d58de1b)




# 
# 

### Part -2 : Placement


After the Floorplan in OpenLANE flow, we just use the command to run Placement as :

    run_placement


![day 2 7](https://github.com/user-attachments/assets/0f657611-b3d6-4a44-b892-125b97721de2)



#### Visualization of the Placement in *Magic* Tool :

To load the generated Placement in magic tool, use this commands as :

    #first change the directory to the generated results directory ../results/placement/ 
    
    cd ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/30-10_10-57/results/placement/
    

    magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &


Screenshots of the Placement :



![day 2 8](https://github.com/user-attachments/assets/8d31d986-5ae1-4f25-ab58-7fe3feb343c1)

# 

![day 2 8 1](https://github.com/user-attachments/assets/c55eea93-e8f4-4b35-b5d4-78fe53608cf7)

#
By Zoom In, we can notice that Standard Cells are placed along the rows.

![day 2 9](https://github.com/user-attachments/assets/1cdd3e3a-a7fd-4852-a930-b97c7c844182)


# 
# 

