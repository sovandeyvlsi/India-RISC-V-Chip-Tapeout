
# India-RISC-V-Chip-Tapeout-Week2

##  BabySoC Fundamentals & Functional Modelling :

### **Part 1 – Theory**
### What is a System-on-Chip (SoC)?

A System on a Chip (SoC) is an integrated circuit (IC) that combines most or all key electronic components of a computer or electronic system into a single, compact microchip.

Essentially, an SoC is a complete, functioning system (or a significant part of one) placed on one chip, unlike traditional systems where components like the CPU, memory, and peripherals are on separate chips on a circuit board.

### Key Components of an SoC
An SoC typically integrates the following main functional units:

**Processor Core(s):** The "brain" of the system, often a Central Processing Unit (CPU), but can also include a Digital Signal Processor (DSP) or a specialized Application-Specific Instruction Set Processor (ASIP).

**Memory:** Built-in memory blocks for storing data and instructions, such as RAM (for fast access) and ROM/Flash/EEPROM (for persistent storage).

**Graphics Processing Unit (GPU):** A dedicated processor for handling graphics and visual output.

**Peripherals or I/O:** Interfaces and controllers for communicating with external devices, such as USB, Wi-Fi, Bluetooth, camera, and display controllers.

**Power Management Unit (PMU):** Circuits to manage and distribute power efficiently across the chip, which is crucial for battery-powered devices.

**Interconnect:** A communication subsystem (like a bus or Network-on-Chip) to connect all the internal components.


### Why BabySoC is a simplified model for learning SoC concepts?

The VSDBabySoC is a simplified model for learning System on a Chip (SoC) concepts because it integrates the core functional blocks of a complex SoC into a minimal, understandable architecture, making the entire design and fabrication process accessible for educational purposes.

#### **Key Features :**

**Minimal Core Components:** A full commercial SoC can have dozens of complex Intellectual Property (IP) cores. The BabySoC significantly reduces this complexity by focusing on just a few critical elements essential for a functioning system, such as:

 A simple RISC-V based processor core (RVMYTH).

A Phase-Locked-Loop (PLL) for clock generation.

A Digital-to-Analog Converter (DAC) to interact with the outside world.

**Focus on Integration:** The model's simplicity highlights the most challenging aspect of SoC design: system integration. By limiting the number of components, students can focus on how the processor, memory, and analog blocks communicate and are physically connected on a single chip, without being overwhelmed by peripheral complexity.

**Open-Source and Fabricatable:** The BabySoC project is designed to be fully open-source and well-documented. It uses standard, open-source toolchains (like OpenLANE) and is often fabricated on accessible technology nodes (like Sky130). This allows students to perform the entire digital design flow, from logic synthesis to physical layout generation (GDSII), which is rare for educational projects.

**Mixed-Signal Design Introduction:** Despite its simplicity, it includes mixed-signal components (PLL and DAC). This provides students with a foundational understanding of how digital and analog circuits must interface and be managed on the same die, a crucial concept in modern SoC design.
        
By keeping the features minimal and the design flow transparent, BabySoC allows students to grasp the entire journey of an SoC—from its architectural concept to its physical layout—in a manageable environment.

Block Diagram of BabySoC :

<img width="2270" height="1260" alt="vsdbabysoc_block_diagram" src="https://github.com/user-attachments/assets/3dfd417f-870c-4b32-97d6-6b55249e926b" />


### The role of functional modelling before RTL and physical design stages:

This early-stage functional modeling focuses on what the chip must do, independent of the actual hardware structure, which prevents costly errors down the line.

**Key Roles of Functional Modeling:**

| Role | Description | Benefit to VLSI Flow |
| :--- | :--- | :--- |
| **Architectural Validation** | The model, typically written in high-level languages like C, C++, or SystemC, describes the **algorithms**, **data flow**, and **control logic** of the system. | **Optimizes the architecture** for performance, power, and area (PPA) before committing to a low-level design. |
| **"Golden" Reference Creation** | The high-level model serves as the **unambiguous, golden reference specification** for the entire project. | **Minimizes the "implementation gap"** by providing a definitive source of truth. |
| **Early Bug Detection** | Functional verification is much **faster and easier to run simulations** and debug at this abstract level. | **Reduces verification cost and time** significantly, as fixing a bug early is cheap. |
| **Testbench Development** | The golden reference model is integrated into the verification environment to automatically **compare the output of the actual RTL design against the expected output**. | **Ensures functional correctness** by automating the checking process. |


# 
# 
# 

### **Part 2 – Labs**

First, we need to install some required packages by the following commands :

    sudo apt install make python3 python3-pip git iverilog gtkwave docker.io python-is-python3

    sudo chmod 666 /var/run/docker.sock

    cd ~

    python3 -m venv ~/virtual_enviornment_directory

    source ~/virtual_enviornment_directory/bin/activate

    pip install pyyaml click sandpiper-saas

    deactivate

Now we can clone the VSDBabySoC repository as :

    git clone https://github.com/manili/VSDBabySoC.git

Now, we can do the Pre Synthesis Simulations (pre_synth_sim) using the *Makefile* script as follows :

    cd VSDBabySoC
    make pre_synth_sim
Otherwise we can do it as follows:

    cd VSDBabySoC

    iverilog -o ../VSDBabySoC/output/pre_synth_sim/ 
    pre_synth_sim.out -DPRE_SYNTH_SIM -I ../VSDBabySoC/src/
    include -I ../VSDBabySoC/src/module ~/VLSI/babysoc/
    VSDBabySoC/src/module/testbench.v -I ~/VLSI/babysoc/
    VSDBabySoC/output/compiled_tlv

    cd output/pre_synth_sim

    ./pre_synth_sim.out

![pre_synth](https://github.com/user-attachments/assets/6ed99899-83d0-42c9-9a3a-3fe80a23b394)


The result of the simulation (i.e. pre_synth_sim.vcd) will be stored in the output/pre_synth_sim directory.

We can now view the waveforms as :

    gtkwave output/pre_synth_sim/pre_synth_sim.vcd

**Output Waveform :**
![baby1](https://github.com/user-attachments/assets/c61f45a5-0835-4e40-99d2-e44cdb7f536c)



## 
**Observations :**

CLK: This signal originates from the PLL block. This is the input CLK signal of the RVMYTH core.

reset: This is the external input reset signal of the RVMYTH core.

OUT: This is the output "OUT" signal of the VSDBabySoC module. This signal comes from the DAC (due to simulation restrictions it behaves like a digital signal which is incorrect).

RV_TO_DAC[9:0]: This is the 10-bit output port of the RVMYTH core, which is fed to DAC block.

OUT: This is a 'real' datatype wire which can simulate analog values. It is the output wire, 'real' datatype OUT signal of the DAC module. This signal comes from the DAC block.

Reset Operation :


![baby2 reset](https://github.com/user-attachments/assets/5e5e4e0c-cb3f-46db-ab55-1f0b4530f6fe)


Observations:

From this Waveform we can clearly see that when the *'reset'* stays high, the *RV_TO_DAC* goes undefined and the corresponding analog output *OUT* stays at zero.
When the *'reset'* goes low, then we can observe that the *RV_TO_DAC* goes to a Specific value and the corresponding analog output *OUT* starts to change. 

But there is a one clock pulse delay in between the reset signal goes low to the changing output signal.  

Clock Signal :

![baby3 clk](https://github.com/user-attachments/assets/dfd6eb6b-0c06-4306-b327-edb629071c49)


Observations :
The clock signal is generated from the PLL block. The PLL block automatically adjusts the frequency and phase of an internal oscillator using a feedback control system  to match the frequency and phase of an external input reference signal.

From this waveform, we can clearly observe that the clock signal initial frequency and phase changes with time initially and then almost fixed to a value after few iterations.  
