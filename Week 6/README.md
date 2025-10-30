# India-RISC-V-Chip-Tapeout-Week6

##  Physical Design Workshop 


### Day 1 : 


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


