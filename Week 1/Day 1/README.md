
# India-RISC-V-Chip-Tapeout-Week1

## Day 1 :
### Lab 1 (D1SK2 L1) : Introduction to Lab

First, create a new directory - 'vsdflow' using command :

        mkdir vsdflow
Then move inside the directory vsdflow using command :

        cd vsdflow

Now clone the git using command :

        git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git

Then inside this sky130RTLDesignAndSynthesisWorkshop directory, we can find all those standard cell library.

Screenshot : 
![cloning git](https://github.com/user-attachments/assets/29cf5a5b-13bb-4a67-a1bb-094f01685e50)


### Lab 2 (D1SK2 L2 Lab2) : Introduction to iverilog gtkwave Part 1

Now we can access all those verilog files in the verilog_files directory inside sky130RTLDesignAndSynthesisWorkshop. 

Now to simulate any verilog file along with its testbench file in iverilog we can use this command :

        iverilog design_file.v testbench.v

For example here, 

        iverilog good_mux.v tb_good_mux.v
Then it will create a.out file and by executing this file it will generate the corresponding .vcd file. 

Now to observe the output waveforms by gtkwave, use command :

        gtkwave file_name.vcd
Here, for example, 
        
        gtkwave tb_good_mux.vcd

Screenshot : 
![cpmplete gtkwave](https://github.com/user-attachments/assets/1ccc8549-5b8e-4b21-8395-3c8776aa635c)


Output Waveform in gtkwave :
![gd mux gtkwave](https://github.com/user-attachments/assets/040200a0-6d21-46c9-a538-efd136e40057)


### Lab 2 (D1SK2 L3 Lab2) : Introduction iverilog gtkwave Part 2

Now look into the design file and the corresponding testbench file by using the command :

        gvim testbench.v -o design_file.v
Here, the command is :

        gvim tb_good_mux.v -o good_mux.v
Then we can look the verilog code of the design file as weel as the testbench file. 

If Command 'gvim' not found ! 
Then install 'gvim' as follows :

        sudo apt install vim-gtk3

Screenshot :
![gvim](https://github.com/user-attachments/assets/fbe378d8-d45b-4b06-9176-eb70abb7c314)


### Lab 3 (D1SK4 L1) : Yosys 1 good mux

First, invoke Yosys by 'yosys' command to synthesize our design.

        yosys
Then select the .lib file as :

         read_liberty -lib /path-of-lib-file/sky130_fd_sc_hd__tt_025C_1v80.lib
Next, select the design file. (Here, good_mux.v)

        read_verilog good_mux.v

Screenshot: 
![synth_yosys](https://github.com/user-attachments/assets/6a7e2bf7-699e-4025-a353-ce9128441717)


Then synthesizing the top module :

        synth -top good_mux

Screenshot:
![synth](https://github.com/user-attachments/assets/9b3ef928-dbb3-4e77-a8d3-3c59311cf55a)


Next, executing technology mapping using ABC:

        abc -liberty /path-of-lib-file/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
Now, we can see the synthesized design as :

        show

Screenshot of the synthesized design :
![synth_final](https://github.com/user-attachments/assets/11b4e726-7663-469d-bf22-d09b42ca51ce)



### Lab 3 (D1SK4 L3) : Yosys 1 good mux

Now, we can write the synthesized netlist as :

         write_verilog good_mux_netlist.v
or

        write_verilog -noattr good_mux_netlist.v

Then we can view the synthesized netlist as :

        !gvim good_mux_netlist.v

Screenshot : 
![netlist](https://github.com/user-attachments/assets/eb0bf30f-42dc-4966-9a8c-db9fd202c556)






