
# India-RISC-V-Chip-Tapeout-Week3

##  Post-Synthesis GLS & STA Fundamentals 


### Part 1 - Post-Synthesis GLS :
Here, we do the Gate Level Simulation (GLS) of the synthesied netlist of the VSDBabySoC.

First, we have to do the Synthesis of the VSDBabySoC using Yosys.
#### Synthesis of the VSDBabySoC using Yosys :

1. Invoke *Yosys* using command :

        yosys
2. Then select all the necessary design files.
    

        read_verilog ../VSDBabySoC/src/module/vsdbabysoc.v
    
        read_verilog -I ../VSDBabySoC/src/include ../VSDBabySoC/   output/compiled_tlv/rvmyth.v

        read_verilog -I ../VSDBabySoC/src/include ../VSDBabySoC/src/module/clk_gate.v


![synth1](https://github.com/user-attachments/assets/3516f180-8366-46a6-99d1-db81de0f1379)


3. Select the .lib files for Synthesis.

        read_liberty -lib ../VSDBabySoC/src/lib/avsdpll.lib
    
        read_liberty -lib ../VSDBabySoC/src/lib/avsddac.lib

        read_liberty -lib ../VSDBabySoC/src/libsky130_fd_sc_hd__tt_025C_1v80.lib


![synth2](https://github.com/user-attachments/assets/9f4d6128-3d75-4bde-8400-2dc6f42bcaa6)


4. Then, synthesizing the top module :

        synth -top vsdbabysoc

Synthesis Statistics :

![new_synth_result1](https://github.com/user-attachments/assets/dd1777c3-33db-4490-86f8-88989a8e421f)


![new_synth_result2](https://github.com/user-attachments/assets/71162ab7-4b94-4281-b894-ac7be6361653)






5. D Flipflop standard cell mapping :

        dfflibmap -liberty ../VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib

6. Logic optimization and Technology mapping :

       opt_clean -purge
       abc -liberty ../VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib

![new_synth_abc](https://github.com/user-attachments/assets/6954e615-8472-4e18-ba3d-e76a3dac251d)



7. Saving the synthesied netlist :

        flatten

        write_verilog -noattr ../VSDBabySoC/output/post_synth/vsdbabysoc.synth.v




8. Check the Synthesis Statistics as :

        stat


![new_synth_result3](https://github.com/user-attachments/assets/cfb75c3b-20ec-48e8-8b44-4985a7fea808)


![new_synth_result4](https://github.com/user-attachments/assets/949c62d0-b4db-48fc-a9d4-019e8e645259)


Generated Netlist :


![new_synth_result5](https://github.com/user-attachments/assets/6ef2c731-7569-4126-8ab9-4dbe718ae029)




#### Gate Level Simulation (GLS) of VSDBabySoC :

1.Here, we do the Gate Level Simulation (GLS) using the iverilog tool as :



      iverilog -o ../VSDBabySoC/output/post_synth/post_synth_sim.out -DPOST_SYNTH_SIM -DFUNCTIONAL -DUNIT_DELAY=#1 -I ../VSDBabySoC/src/include -I ../VSDBabySoC/src/module -I ../VSDBabySoC/src/gls_model ~/VLSI/babysoc/VSDBabySoC/src/module/testbench.v -I ~/VLSI/babysoc/VSDBabySoC/output/post_synth





2. Then go to the output directory (*post_synth*) and run the simulation as :

        cd output/post_synth/

        ./post_synth_sim.out
3. Now, we can view the GLS output waveform as :

        gtkwave post_synth_sim.vcd

![new_synth_result5 5](https://github.com/user-attachments/assets/d020952a-307e-44fe-84f7-b8502e146a3a)


![new_synth_result_final](https://github.com/user-attachments/assets/329723f8-52cd-4776-befe-e4f3ee50ecae)



GLS Output Waveform :


![new_synth_result6](https://github.com/user-attachments/assets/36051464-f0c9-4d7d-b3c8-2518163c5069)



4. Now, by comparing the GLS output waveform with the Functional simulated output waveform (See, [Week 2 Lab](https://github.com/sovandeyvlsi/India-RISC-V-Chip-Tapeout/tree/main/Week%202#part-2--labs)), we can say that both have the save output waveform. 
