
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




