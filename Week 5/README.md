# India-RISC-V-Chip-Tapeout-Week5

## OpenROAD Installation 


### Step 1 : Clone Repository


First Clone the github Repository as :

    git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts

    cd OpenROAD-flow-scripts

![openroad flow 1](https://github.com/user-attachments/assets/49e64328-f551-4622-8fef-e629b3b930a0)



### Step 2 : Run the Setup Script

    sudo ./setup.sh


### Step 3 : Build OpenROAD

    ./build_openroad.sh --local

Then, 

    source ./env.sh

### Step 4 : Verify Installation

    $OPENROAD_CMD -version
and

    yosys -V



![openroad flow verify](https://github.com/user-attachments/assets/5cc868de-d716-4669-ba73-6802cdd1e861)




### Problems may arise at the time of Installation :

Though in the OpenROAD-flow-scrips all the dependencies are there, but sometimes there may occur dependencies problems, especially the version mismatch between the dependencies and the OpenROAD installer. 



![openroad flow 2](https://github.com/user-attachments/assets/114562d3-76b5-43cf-82a2-87a523f76cd1)




After properly installing that particular dependency version, we restart the again the Building the OpenROAD at *OpenROAD-flow-scripts/* directory.



![openroad flow 3](https://github.com/user-attachments/assets/78182e94-e483-4b43-8997-c9e882e9f07d)






### Step 5 : Running the OpenROAD Flow

Using the *makefile* scripts, run the OpenROAD flow as :

    cd OpenROAD-flow-scripts/flow
    make


![openroad flow 4 0](https://github.com/user-attachments/assets/a74618fe-5c2f-43ef-ade1-40c6f1aae2ad)




### Step 6 : Launch the Graphical User Interface (GUI)

To visualize the layout launch the GUI as :

     make gui_final



![openroad flow 3 1](https://github.com/user-attachments/assets/ea8ad7f4-4479-48e4-b3a9-f0320084dd67)



Screenshot of the Layout :


![openroad flow 4](https://github.com/user-attachments/assets/57142267-3ed8-4cda-bac2-052be7ea3b46)




