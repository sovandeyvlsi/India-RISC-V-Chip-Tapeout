
# India-RISC-V-Chip-Tapeout-Week1

## Day 2 :
### Lab 4 : Introduction to dot Lib (.lib)

Here we will explore our open source library file sky130_fd_sc_hd__tt_025C_1v80.lib 

tt signifies the fabrication process : Typical process

025C signifies the parameters in the library is with the reference of 25° C. 

1v80 signifies the core operating voltage of 1.8 V

To view the .lib file we can use command as :

        gvim sky130_fd_sc_hd__tt_025C_1v80.lib

Screenshot of the .lib file :
![lib](https://github.com/user-attachments/assets/f7af4523-6bd6-48e4-b7b9-8a292710944f)


### Lab 5 : Hierarchical Synthesis vs Flat Synthesis

Here, first we will do Hierarchical Synthesis of a module with multiple submodules.

Screenshot of the 'multiple_modules.v' :
![multiple_modules](https://github.com/user-attachments/assets/386e0bf7-92be-4480-a9a7-9b152a4e9245)


Now, we do the Hierarchical Synthesis of the 'multiple_modules.v' in yosys as the steps mentioned in Lab 3.
Screenshots :
![result1](https://github.com/user-attachments/assets/28322d06-5c90-4f10-afb9-15f82fd622b7)

![result2](https://github.com/user-attachments/assets/323562f4-87c1-4025-98c5-2c2b3cdb0693)

![abc result](https://github.com/user-attachments/assets/19f5fcaa-0b02-47c5-8ab5-768442881b6c)



We can show the Synthesised design by command :

        show multiple_modules

Screenshot:

![hier](https://github.com/user-attachments/assets/1fa6b99e-89ef-4d59-83e5-3368b1b8bf89)


We save the Synthesised netlist as :

        write_verilog -noattr multiple_modules_hier.v
Open the netlist as :

        !gvim multiple_modules_hier.v 
Screenshot:
![hier2](https://github.com/user-attachments/assets/eb0bd0ca-bc2f-4f7b-867c-eac85a811108)


Now, we do the Flat Synthesis :
While doing the synthesis as mentioned in Lab 3, we do till the 'abc -liberty ..' and then command :

        flatten
Then 

        show multiple_modules

Screenshot:
![flat1](https://github.com/user-attachments/assets/e3577998-b6f7-414a-89fe-1e6be53e5b95)


Save the Synthesised flatten netlist as :

        write_verilog -noattr multiple_modules_flat.v
Open the flatten netlist as :

        !gvim multiple_modules_flat.v
Screenshot :
![flat2](https://github.com/user-attachments/assets/9d43603f-af76-4c7c-82f7-3a0cbee72668)


### Lab : Various flops coding styles and optimizations :
### (D2SK3) Lab flop synthesis simulations :

### Simulations :

 #### 1. D-Flipflop with asynchronus reset :
 First we do the simulation of the design file 'dff_asyncres.v' along with its testbench 'tb_dff_asyncres.v' using iverilog and visualize the waveform using gtkwave as described in [Lab 2.](https://github.com/sovandeyvlsi/India-RISC-V-Chip-Tapeout/tree/main/Week%201/Day%201#lab-2-d1sk2-l2-lab2--introduction-to-iverilog-gtkwave-part-1) (You can click on 'Lab 2' and see the process steps)

Verilog file :

![async reset](https://github.com/user-attachments/assets/b36cb3ba-31f3-474c-92ae-fbfc0a144aad)


Output waveform :
![async reset gtk](https://github.com/user-attachments/assets/a7ac9136-28c4-4b65-94fb-d4d62883224f)



#### 2. D-Flipflop with asynchronus set :
Now, we do the simulation of the design file 'dff_async_set.v' along with its testbench 'tb_dff_async_set.v' using iverilog and visualize the waveform using gtkwave. 

Verilog file :
![async set 0](https://github.com/user-attachments/assets/407f3362-c91b-4662-b5d3-9748849cf1d3)


Output waveform :
![async set](https://github.com/user-attachments/assets/8ab2c57f-757f-41b0-9304-8945eb024d0f)


#### 3. D-Flipflop with synchronus reset :
Here the reset is synchronused with the clock. 

Verilog file :
![syn reset](https://github.com/user-attachments/assets/9c851755-b6b7-45fc-87ca-9f952efd628b)


Output waveform :
![syn reset 2](https://github.com/user-attachments/assets/a716c69a-035e-4150-9561-7669a77c15aa)



### Synthesis :

Here, now we will the do the synthesis of the mentioned three designs using Yosys. For the process steps we can refer the steps mentioned in [Lab 3.](https://github.com/sovandeyvlsi/India-RISC-V-Chip-Tapeout/tree/main/Week%201/Day%201#lab-3-d1sk4-l1--yosys-1-good-mux)

Here, in the synthesis steps, we add an aditional step of D Flipflop library mapping after the *"synth - top design_file"* as :

        dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

 #### 1. Synthesised Design of  D-Flipflop with asynchronus reset :
![synth 1 asnc reset](https://github.com/user-attachments/assets/db7f7c02-fc06-404a-bb19-a5288ee85f12)


#### 2. Synthesized Design D-Flipflop with asynchronus set :
![synth 2 asnc set](https://github.com/user-attachments/assets/980f812e-1667-4f29-982b-f75a829e2aea)


#### 3. Synthesized Design of D-Flipflop with synchronus reset :
![synth 3 sync reset](https://github.com/user-attachments/assets/3d481533-aa5f-4cde-a129-2db39f32266a)





