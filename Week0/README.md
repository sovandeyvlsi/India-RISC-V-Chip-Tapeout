
# India-RISC-V-Chip-Tapeout-Week0 : Task 0
## Task-1 : Create GitHub repo.
Here is my Github Repository : 


## Task-2 : Install Tools :

### 1. Ubuntu :
Installing Ubuntu on Windows 11 using WSL2.
  
  Open PowerShell as Administrator.
  
  Run the WSL Installation Command:

    wsl --install

This command will automatically enable the required Windows features (Windows Subsystem for Linux and Virtual Machine Platform), download the latest Linux kernel, and install the Ubuntu distribution.

Restart Your Computer.

Create a New User: Create a new Unix username and password.

Update the package list: 

    sudo apt update
Upgrade the packages:

    sudo apt upgrade -y

Installation Process Screenshot :

![ubuntu process](https://github.com/user-attachments/assets/88127c96-14bc-4c74-9950-dab3791c55fb)


Check installed Ubuntu Version using :

    lsb_release -a



![ubuntu](https://github.com/user-attachments/assets/f548d822-99be-4c95-8276-54d16df63ceb)



### 2. Yosys :
To install Yosys in Ubuntu, follow these steps -

    sudo apt-get install yosys

Installing Prerequisites:

    sudo apt-get install gperf build-essential clang lld bison flex libfl-dev libreadline-dev gawk tcl-dev libffi-dev git graphviz xdot pkg-config python3 libboost-system-dev libboost-python-dev libboost-filesystem-dev zlib1g-dev

Clone the Repository:

    git clone --recurse-submodules https://github.com/YosysHQ/yosys.git

Build and Install:

    cd yosys
    make
    sudo make install

After the installation is complete, run Yosys by: 

    yosys

Screenshot of the launched Yosys shell :



![yosys](https://github.com/user-attachments/assets/8652ca73-04f6-41c7-8a14-2050ed335d07)


### 3. Iverilog :
To install Iverilog, follow these steps -

Update the package list: 

    sudo apt update
Install Iverilog :

    sudo apt install iverilog

Verify the installation:

    iverilog -V

Screenshot of the installed Iverilog : 



![iverilog](https://github.com/user-attachments/assets/d6c7b842-4dba-4e63-9c0e-b5205b5ced19)


### 4. gtkwave :
To install Iverilog, follow these steps -

Update the package list: 

    sudo apt update
Install Iverilog :

    sudo apt install gtkwave

Verify the installation:

    gtkwave --version

Screenshot of the installed gtkwave :



![gtkwave](https://github.com/user-attachments/assets/025a09f6-eaa7-4685-9f57-204969095a0e)



