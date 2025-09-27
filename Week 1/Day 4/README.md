
# India-RISC-V-Chip-Tapeout-Week1

## Day 4 :
### Lab : GLS Synthesis Simulation Mismatch

Here, first we do the RTL simulation of some circuits and then we do the synthesis and generate gate-level netlist. Next we do the Gate Level Simulation (GLS) of the generated netlist and check the functionalities.
We will follow the RTL simulation steps mentioned in [Lab 2](https://github.com/sovandeyvlsi/India-RISC-V-Chip-Tapeout/tree/main/Week%201/Day%201#lab-2-d1sk2-l2-lab2--introduction-to-iverilog-gtkwave-part-1) and also follow the synthesis steps as mentioned in [Lab 3.](https://github.com/sovandeyvlsi/India-RISC-V-Chip-Tapeout/tree/main/Week%201/Day%201#lab-3-d1sk4-l1--yosys-1-good-mux)

For Gate Level Simulation (GLS), we follow this steps :

    iverilog ../my_lib/verilog_model/primitives.v  ../my_lib/verilog_model/sky130_fd_sc_hd.v generated_netlist.v testbench.v

    ./a.out

    gtkwave testbench.vcd


#### Circuit 1 : ternary_operator_mux.v
Verilog Code :

![ternary1](https://github.com/user-attachments/assets/788542e8-8800-4bfc-9b7b-d54102c768b0)


RTL Simulated Output Waveform :

![ternary2](https://github.com/user-attachments/assets/cfb34332-5dac-4880-9beb-eaa4acd0f557)


Synthesized Circuit :

![ternary3](https://github.com/user-attachments/assets/651315b9-a5ba-4346-8dee-c3116a180a14)


Synthesized Netlist :

![ternary4](https://github.com/user-attachments/assets/7b7ccd75-2ff9-470a-b427-f30ebccabfc5)


Gate Level Simulation (GLS) Output Waveform :


![ternary5](https://github.com/user-attachments/assets/698bbd8e-a79a-4dbd-acc8-fea0887ade85)


# 
# 

#### Circuit 2 : bad_mux.v
Verilog Code :


![bad_mux1](https://github.com/user-attachments/assets/2b3cb5f9-9c83-4c2c-b3cb-a968e6867905)


RTL Simulated Output Waveform :

![bad_mux2](https://github.com/user-attachments/assets/28c7102c-2f7d-47d6-a820-9f3c18c3e1fe)


Synthesized Circuit :

![bad_mux3](https://github.com/user-attachments/assets/0a43edc0-0458-46d7-b759-44424206af8d)


Synthesized Netlist :


![bad_mux4](https://github.com/user-attachments/assets/b9489a96-1a6a-47d5-843c-4f0fc373c486)


Gate Level Simulation (GLS) Output Waveform :


![bad_mux5](https://github.com/user-attachments/assets/261dd8f0-a235-4131-9908-c75ed28dff7f)


* Here we can notice that there is a mismatch between the RTL Simulated Output Waveform and Gate Level Simulation (GLS) Output Waveform. That's the GLS Synthesis Simulation Mismatch.


# 
#  
# 

### Lab : Synthesis Simulation Mismatch Blocking Statement


