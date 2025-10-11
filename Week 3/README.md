
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


![new_synth_result5 6](https://github.com/user-attachments/assets/c02d2cc3-9a66-4976-8cd2-f8bc2bbfe461)





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



#### Alternative Process using the *Makefile* Scripts :
Now, all these steps can be done simply by using the *makefile* scripts as :

        cd ~/VLSI/babysoc/VSDBabySoC

        make synth

        make post_synth_sim

        gtkwave output/post_synth_sim/post_synth_sim.vcd




**GLS Output Waveform :**



![new_synth_result7](https://github.com/user-attachments/assets/23c07820-4359-40ca-9f6c-90f33a061af5)



4. Now, by comparing the GLS output waveform with the Functional simulated output waveform (See, [Week 2 Lab](https://github.com/sovandeyvlsi/India-RISC-V-Chip-Tapeout/tree/main/Week%202#part-2--labs)), we can say that both have the save output waveform. 






### Part 3 – Generate Timing Graphs with OpenSTA :

### Installation of OpenSTA :
First, we have to install the OpenSTA. For this we have to follow these steps :

Step 1 : Install all necessary compiler tools and libraries

        
    sudo apt update

    sudo apt install -y build-essential

    sudo apt install -y cmake git tcl-dev swig bison flex libeigen3-dev libz-dev

Step 2 : Clone the source code from the official GitHub repository

    cd ~
    git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
    cd OpenSTA


Step 3: Build and Compile OpenSTA

    mkdir build
    cd build
    cmake ..
    make -j$(nproc)

Step 4 : Add to System PATH and Launch :

    echo 'export PATH=$HOME/OpenSTA/build/app:$PATH' >> ~/.bashrc
    source ~/.bashrc

Now, we can start the OpenSTA tool from any location by simply typing:

    sta

### Static Timing Analysis of VSDBabySoC using OpenSTA :

First invoke the OpenSTA tool as :

    sta

Then follow this commands as :

    read_liberty -min ../VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    read_liberty -max ../VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    read_liberty -min ../VSDBabySoC/src/lib/avsdpll1.lib
    read_liberty -max ../VSDBabySoC/src/lib/avsdpll1.lib
    read_liberty -min ../VSDBabySoC/src/lib/avsddac.lib
    read_liberty -max ../VSDBabySoC/src/lib/avsddac.lib
    read_verilog ../VSDBabySoC/output/post_synth/vsdbabysoc.synth.v
    link_design vsdbabysoc
    read_sdc ../VSDBabySoC/src/sdc/vsdbabysoc_synthesis.sdc
    report_checks

![baby_sta1](https://github.com/user-attachments/assets/bbd640a5-65ef-42ea-81f9-2085dbada247)


![baby_sta2](https://github.com/user-attachments/assets/b79ae938-7c56-4949-a07f-951564df1eee)




We can do the *setup* and *hold* check as :

    report_checks -path_delay min_max



![baby_sta3 min](https://github.com/user-attachments/assets/801e9746-0cf8-44ff-8c90-f075a610d2de)


![baby_sta3 max](https://github.com/user-attachments/assets/57e4ab16-aed7-454d-9be9-0262f99057fd)



### PVT Corner Analysis of VSDBabySoC:

STA is performed across all PVT corners to validate that the design meets timing requirements.

The timing libraries (all the PVT corners) can be clonned from this repo :

https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd.git



Now, we create a TCL script that can be executed to perform STA for the available PVT corners using the Sky130 timing libraries.

The TCL script :

    set list_of_lib_files(1) "sky130_fd_sc_hd__tt_025C_1v80.lib"
    set list_of_lib_files(2) "sky130_fd_sc_hd__ff_100C_1v65.lib"
    set list_of_lib_files(3) "sky130_fd_sc_hd__ff_100C_1v95.lib"
    set list_of_lib_files(4) "sky130_fd_sc_hd__ff_n40C_1v56.lib"
    set list_of_lib_files(5) "sky130_fd_sc_hd__ff_n40C_1v65.lib"
    set list_of_lib_files(6) "sky130_fd_sc_hd__ff_n40C_1v76.lib"
    set list_of_lib_files(7) "sky130_fd_sc_hd__ss_100C_1v40.lib"
    set list_of_lib_files(8) "sky130_fd_sc_hd__ss_100C_1v60.lib"
    set list_of_lib_files(9) "sky130_fd_sc_hd__ss_n40C_1v28.lib"
    set list_of_lib_files(10) "sky130_fd_sc_hd__ss_n40C_1v35.lib"
    set list_of_lib_files(11) "sky130_fd_sc_hd__ss_n40C_1v40.lib"
    set list_of_lib_files(12) "sky130_fd_sc_hd__ss_n40C_1v44.lib"
    set list_of_lib_files(13) "sky130_fd_sc_hd__ss_n40C_1v76.lib"

    read_liberty ~/VLSI/babysoc/VSDBabySoC/src/lib/avsdpll1.lib
    read_liberty ~/VLSI/babysoc/VSDBabySoC/src/lib/avsddac.lib

    for {set i 1} {$i <= [array size list_of_lib_files]} {incr i} {
    read_liberty ~/VLSI/babysoc/VSDBabySoC/src/lib/pdk/ skywater-pdk-libs-sky130_fd_sc_hd/timing/$list_of_lib_files($i)
    read_verilog ~/VLSI/babysoc/VSDBabySoC/output/post_synth/vsdbabysoc.synth.v
    link_design vsdbabysoc
    read_sdc ~/VLSI/babysoc/VSDBabySoC/src/sdc/vsdbabysoc_synthesis.sdc
    check_setup -verbose
    report_checks -path_delay min_max -fields {nets cap slew input_pins fanout} -digits {4} > ~/VLSI/babysoc/VSDBabySoC/output/sta/sta_output/min_max_$list_of_lib_files($i).txt

    exec echo "$list_of_lib_files($i)" >> ~/VLSI/babysoc/VSDBabySoC/output/sta/sta_output/sta_worst_max_slack.txt
    report_worst_slack -max -digits {4} >> ~/VLSI/babysoc/VSDBabySoC/output/sta/sta_output/sta_worst_max_slack.txt

    exec echo "$list_of_lib_files($i)" >> ~/VLSI/babysoc/VSDBabySoC/output/sta/sta_output/sta_worst_min_slack.txt
    report_worst_slack -min -digits {4} >> ~/VLSI/babysoc/VSDBabySoC/output/sta/sta_output/sta_worst_min_slack.txt

    exec echo "$list_of_lib_files($i)" >> ~/VLSI/babysoc/VSDBabySoC/output/sta/sta_output/sta_tns.txt
    report_tns -digits {4} >> ~/VLSI/babysoc/VSDBabySoC/output/sta/sta_output/sta_tns.txt

    exec echo "$list_of_lib_files($i)" >> ~/VLSI/babysoc/VSDBabySoC/output/sta/sta_output/sta_wns.txt
    report_wns -digits {4} >> ~/VLSI/babysoc/VSDBabySoC/output/sta/sta_output/sta_wns.txt
    }


![tcl](https://github.com/user-attachments/assets/cbe9ae36-1a7c-49e6-ace4-a2267bc286d8)



Now invoke the OpenSTA tool and run the TCL script as :

    sta
    source ../VSDBabySoC/sta_pvt.tcl

All the generated reports are stored at location *..VSDBabySoC/output/sta/sta_output/*

Then plot the reports using python scipts.


![pvt 1](https://github.com/user-attachments/assets/5dd8e96f-26e5-46be-b7dc-e117891c835c)








Combined Report Table :


| Library / Corner | Worst Max Slack (Setup) [ns] | Worst Min Slack (Hold) [ns] | WNS [ns] | TNS [ns] | Status (WNS) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **sky130_fd_sc_hd__tt_025C_1v80** | 1.8865 | 0.3096 | 0.0000 | 0.0000 | ✅ PASS |
| **sky130_fd_sc_hd__ff_100C_1v65** | 3.7904 | 0.2491 | 0.0000 | 0.0000 | ✅ PASS |
| **sky130_fd_sc_hd__ff_100C_1v95** | 5.3898 | 0.1960 | 0.0000 | 0.0000 | ✅ PASS |
| **sky130_fd_sc_hd__ff_n40C_1v56** | 0.9227 | 0.2915 | 0.0000 | 0.0000 | ✅ PASS |
| **sky130_fd_sc_hd__ff_n40C_1v65** | 2.4592 | 0.2551 | 0.0000 | 0.0000 | ✅ PASS |
| **sky130_fd_sc_hd__ff_n40C_1v76** | 3.7081 | 0.2243 | 0.0000 | 0.0000 | ✅ PASS |
| **sky130_fd_sc_hd__ss_n40C_1v76** | -5.8387 | 0.5038 | -5.8387 | -3236.4844 | ❌ FAIL |
| **sky130_fd_sc_hd__ss_100C_1v60** | -6.5819 | 0.6420 | -6.5819 | -3565.8271 | ❌ FAIL |
| **sky130_fd_sc_hd__ss_100C_1v40** | -15.0265 | 0.9053 | -15.0265 | -9746.8154 | ❌ FAIL |
| **sky130_fd_sc_hd__ss_n40C_1v44** | -23.6693 | 0.9909 | -23.6693 | -18547.2090 | ❌ FAIL |
| **sky130_fd_sc_hd__ss_n40C_1v40** | -27.7760 | 1.1249 | -27.7760 | -22631.8301 | ❌ FAIL |
| **sky130_fd_sc_hd__ss_n40C_1v35** | -36.3514 | 1.3475 | -36.3514 | -30164.3398 | ❌ FAIL |
| **sky130_fd_sc_hd__ss_n40C_1v28** | -56.3915 | 1.8296 | -56.3915 | -48818.3672 | ❌ FAIL |



Worst Max Slack (Setup) Plot :

<img width="1400" height="1200" alt="setup slack" src="https://github.com/user-attachments/assets/9809ffba-78ac-4d33-9ccf-db64578f0669" />


Worst Min Slack (Hold) Plot :

<img width="1400" height="1200" alt="hold slack" src="https://github.com/user-attachments/assets/9d65ffbe-bd35-4e95-8e8b-2f47644c5968" />


WNS Plot :


<img width="1400" height="1200" alt="WNS" src="https://github.com/user-attachments/assets/aa8322f1-a6bb-4e29-b4d6-dfd6d315358f" />


TNS Plot :


<img width="1400" height="1200" alt="TNS" src="https://github.com/user-attachments/assets/11bd8c1c-023f-44a6-866b-c3dfed24f78d" />



