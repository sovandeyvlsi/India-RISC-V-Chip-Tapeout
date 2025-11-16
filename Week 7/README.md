
# India-RISC-V-Chip-Tapeout-Week7

##  BabySoC Physical Design & Post-Route SPEF Generation



First, we have to create a directory named *vsdbabysoc* inside the *OpenROAD-flow-scripts/flow/designs/sky130hd/* by using this command :

    cd ~/OpenROAD-flow-scripts/flow/designs/sky130hd/
    mkdir vsdbabysoc

Then we copy the folders **gds**, **include**, **lef** and **lib** from the VSDBabySoC directory. 

Make sure those folders contains these files as :

**gds** : avsddac.gds, avsdpll.gds

**include** : sandpiper.vh, sandpiper_gen.vh, sp_default.vh and sp_verilog.vh

**lef** : avsddac.lef and avsdpll.lef

**lib** : avsddac.lib and avsdpll.lib only.

Next copy the design constraints file **vsdbabysoc_synthesis.sdc** from VSDBabySoC directory.

Then also copy the **macro.cfg** and **pin_order.cfg** from the VSDBabySoC directory.



Now, create a folder named *vsdbabysoc* inside the *OpenROAD-flow-scripts/flow/designs/src/* directory as :

    cd ~/OpenROAD-flow-scripts/flow/designs/src/
    mkdir vsdbabysoc

Then copy all the necessary verilog files from the VSDBabySoC directory inside this *../src/vsdbabysoc/* directory.

This folder should contain these files :

**vsdbabysoc.v**

**rvmyth.v**

**avsddac.v**

**avsdpll.v**

**rvmyth_gen.v**

**clk_gate.v**




Finally, create a **config.mk** file inside the *~/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc* directory using gvim or gedit. And the content of this file should be as :

    export DESIGN_NICKNAME = vsdbabysoc
    export DESIGN_NAME = vsdbabysoc
    export PLATFORM    = sky130hd

    # export VERILOG_FILES_BLACKBOX = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/IPs/*.v
    # export VERILOG_FILES = $(sort $(wildcard $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/*.v))
    # Explicitly list the Verilog files for synthesis
    export VERILOG_FILES = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/vsdbabysoc.v \
                        $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/rvmyth.v \
                        $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/clk_gate.v

    export SDC_FILE      = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/vsdbabysoc_synthesis.sdc

    export vsdbabysoc_DIR = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)

    export VERILOG_INCLUDE_DIRS = $(wildcard $(vsdbabysoc_DIR)/include/)
    # export SDC_FILE      = $(wildcard $(vsdbabysoc_DIR)/sdc/*.sdc)
    export ADDITIONAL_GDS  = $(wildcard $(vsdbabysoc_DIR)/gds/*.gds.gz)
    export ADDITIONAL_LEFS  = $(wildcard $(vsdbabysoc_DIR)/lef/*.lef)
    export ADDITIONAL_LIBS = $(wildcard $(vsdbabysoc_DIR)/lib/*.lib)
    export PDN_TCL = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/pdn.tcl

    # Clock Configuration (vsdbabysoc specific)
    # export CLOCK_PERIOD = 20.0
    export CLOCK_PORT = CLK
    export CLOCK_NET = $(CLOCK_PORT)

    # Floorplanning Configuration (vsdbabysoc specific)
    export FP_PIN_ORDER_CFG = $(wildcard $(DESIGN_DIR)/pin_order.cfg)
    # export FP_SIZING = absolute

    export DIE_AREA   = 0 0 1600 1600
    export CORE_AREA  = 20 20 1590 1590

    # Placement Configuration (vsdbabysoc specific)
    export MACRO_PLACEMENT_CFG = $(wildcard $(DESIGN_DIR)/macro.cfg)
    export PLACE_PINS_ARGS = -exclude left:0-600 -exclude left:1000-1600: -exclude right:* -exclude top:* -exclude bottom:*
    # export MACRO_PLACEMENT = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/macro_placement.cfg

    export TNS_END_PERCENT = 100
    export REMOVE_ABC_BUFFERS = 1

    # Magic Tool Configuration
    export MAGIC_ZEROIZE_ORIGIN = 0
    export MAGIC_EXT_USE_GDS = 1

    # CTS tuning
    export CTS_BUF_DISTANCE = 600
    export SKIP_GATE_CLONING = 1

    # export CORE_UTILIZATION=0.1  # Reduce this value to allow more whitespace for routing.




### Synthesis :

Now go to the *OpenROAD-flow-scripts/flow* directory in the terminal and then run synthesis command as :

    make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk synth


**Screenshots :**


![w7 1](https://github.com/user-attachments/assets/3b8549aa-75bb-4f99-8979-191bd6e60a74)


![w7 2](https://github.com/user-attachments/assets/256488cf-cc84-419a-bd7c-b9a15db0b5c0)



**Synthesis Netlist :**


![w7 3 1](https://github.com/user-attachments/assets/190924ec-6016-441a-af1c-1db71cfa9fbd)



**Synthesis Statistics :**

![w7 4 1](https://github.com/user-attachments/assets/7d922c36-08c6-462e-bba2-fce93fa00406)



![w7 4 2](https://github.com/user-attachments/assets/45cdc551-3c41-4e2f-95fb-9a63a60602fa)



### Floorplan :

Next we use the command for Floorplan as :

    make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk floorplan

**Screenshots :**

![w7 5](https://github.com/user-attachments/assets/3ef89936-f1a0-41b7-99ce-1ff75d2cbc39)



To view the floorplan in GUI mode, use the command as :

    make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_floorplan

**Screenshots :**


![w7 6](https://github.com/user-attachments/assets/47b4faa9-c518-4494-8159-0fc966023afa)


![w7 7 floorplan](https://github.com/user-attachments/assets/ccc252ea-18fe-41b2-9363-7ec625055a3f)


# 

### Placement :

Then for the placement use the command as :

    make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk place

**Screenshots :**

![w7 8](https://github.com/user-attachments/assets/c57c821c-ba40-4ccf-ab3e-e8c3017111a9)




To view the placement in GUI mode, use the command as :

    make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_place

**Screenshots :**


![w7 9](https://github.com/user-attachments/assets/c25366a0-d0d7-46af-8bd1-eb1ceb01411a)

# 


![w7 10 place](https://github.com/user-attachments/assets/8715732c-da78-4182-a84a-b562f307e985)


# 


We can observe the Placement Heatmap by just clicking on the Heatmap option in OpenROAD gui interface.

**Screenshots :**



![w7 11 heatmap](https://github.com/user-attachments/assets/e84a2536-0321-48f2-bcd6-0a6e7264ca50)


# 

![w7 12](https://github.com/user-attachments/assets/1315f0a2-3230-4b8d-abda-4aa6cb5769e8)


# 

![w7 13](https://github.com/user-attachments/assets/8bfcd689-7581-48aa-ab1b-4d965e1bd082)

# 


### Clock Tree Synthesis(CTS) :

To do the CTS, we use the command as :

    make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk cts





To view the CTS in GUI mode, use the command as :

    make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_cts


**Screenshots :**

![w7 14](https://github.com/user-attachments/assets/0cecc7b8-cb30-4477-9c83-f77d4683a33e)

# 
![w7 15](https://github.com/user-attachments/assets/c15fa0d4-7512-414c-bc3c-3cd80bfaf9bd)

# 

![w7 16](https://github.com/user-attachments/assets/aac52661-c769-4b4d-ae6d-a45bad297f9b)

# 


Also we can observe the CTS reports inside the directory *./flow/reports/sky130hd/vsdbabysoc/base/* .

**Screenshots :**


![w7 17](https://github.com/user-attachments/assets/9a725f08-072f-428f-ae93-b4e6a3939796)

# 


### Routing :

For routing we use the command as :

    make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk route


**Screenshots :**

![w7 18](https://github.com/user-attachments/assets/1f713bf2-8a3e-4e2a-9a02-1d764779b257)

# 

![w7 19](https://github.com/user-attachments/assets/fcb9e703-dcb8-4ed5-815c-c23ce6bd004b)

# 




Here, we got some congestion regions. We opened the OpenROAD gui and load the the previous CTS .obd files in the DRC Viewer. 

**Screenshots :**

![w7 20 drc](https://github.com/user-attachments/assets/a37f84a7-6c5e-45be-a817-2490d1bfe6bf)


# 



