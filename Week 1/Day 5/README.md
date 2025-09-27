# India-RISC-V-Chip-Tapeout-Week1

## Day 5 :
### Lab : Incomplete IF

Here, first we do the RTL simulation and synthesis of some circuits where Incomplete IF statements can inferred some latches. 
We will follow the RTL simulation steps mentioned in [Lab 2](https://github.com/sovandeyvlsi/India-RISC-V-Chip-Tapeout/tree/main/Week%201/Day%201#lab-2-d1sk2-l2-lab2--introduction-to-iverilog-gtkwave-part-1) and also follow the synthesis steps as mentioned in [Lab 3.](https://github.com/sovandeyvlsi/India-RISC-V-Chip-Tapeout/tree/main/Week%201/Day%201#lab-3-d1sk4-l1--yosys-1-good-mux)


#### Circuit 1 : incomp_if.v
Verilog Code :

![incomp_if1](https://github.com/user-attachments/assets/1ee9cedb-2e0e-459b-ba57-b6446b103866)


Simulated Output Waveform :

![incomp_if2](https://github.com/user-attachments/assets/cc53c5bd-2ec4-4adb-9b1f-c2750e36797f)


Synthesized Circuit :

![incomp_if3](https://github.com/user-attachments/assets/d1de78ca-346c-4e15-90f8-3d4eea23ab87)




#### Circuit 2 : incomp_if2.v
Verilog Code :


![incomp_if 21](https://github.com/user-attachments/assets/3daaaa5d-5a89-47ec-8021-a8dd99c1a3cf)


Simulated Output Waveform :


![incomp_if 22](https://github.com/user-attachments/assets/ffa514ff-bc72-4acc-98ff-7704b124dccd)


Synthesized Circuit :

![incomp_if 23](https://github.com/user-attachments/assets/0d5ee2d3-e218-48f9-b76b-1f1e36f48c3e)




# 
#  
# 
### Lab : Incomplete Overlapping CASE



#### Circuit 1 : incomp_case.v
Verilog Code :

![incomp_case1](https://github.com/user-attachments/assets/65f4bc8d-5ceb-464d-a50d-dc0b433818fd)


Simulated Output Waveform :

![incomp_case2](https://github.com/user-attachments/assets/5f33a036-0197-481c-b398-42e6b5b5f847)


Synthesized Circuit :

![incomp_case3](https://github.com/user-attachments/assets/dbe44dbf-1a54-4c66-9b51-efa4e6c7d483)


#### Circuit 2 : comp_case.v
Verilog Code :

![comp_case1](https://github.com/user-attachments/assets/4040e7f5-8a2b-4c95-a84c-744beb687501)


Simulated Output Waveform :


![comp_case2](https://github.com/user-attachments/assets/db36f701-e805-4b91-9f50-34cfae60d738)


Synthesized Circuit :

![comp_case3](https://github.com/user-attachments/assets/7a5dcd49-1432-4672-8a05-98f20f224d0b)



#### Circuit 3 : bad_case.v
Verilog Code :

![bad_case1](https://github.com/user-attachments/assets/fd33e2f5-d089-47d8-9a67-14e3c53d7eaa)


RTL Simulated Output Waveform :


![bad_case2](https://github.com/user-attachments/assets/cf1efc8c-fa60-4650-a991-5a59202ec712)


Synthesized Circuit :


![bad_case3](https://github.com/user-attachments/assets/be64ca0d-6bc9-4fe8-8476-bdfe795eab28)


Synthesized Netlist :


![bad_case4](https://github.com/user-attachments/assets/c615a6bc-c02f-4ecb-9625-21392b961493)


Gate Level Simulation (GLS) Output Waveform :


![bad_case5](https://github.com/user-attachments/assets/9261b121-e7ae-4791-9c54-b5d578b6aa23)


* Here we can notice that there is a  GLS Synthesis Simulation Mismatch between the RTL Simulated Output Waveform and Gate Level Simulation (GLS) Output Waveform.




# 
#  
# 

### Lab : For and For Generate

First, here we do simulation and synthesis of some verilog modules in which 'for' loops are used.

We will follow the RTL simulation steps mentioned in [Lab 2](https://github.com/sovandeyvlsi/India-RISC-V-Chip-Tapeout/tree/main/Week%201/Day%201#lab-2-d1sk2-l2-lab2--introduction-to-iverilog-gtkwave-part-1) and also follow the synthesis steps as mentioned in [Lab 3.](https://github.com/sovandeyvlsi/India-RISC-V-Chip-Tapeout/tree/main/Week%201/Day%201#lab-3-d1sk4-l1--yosys-1-good-mux)



#### Design 1 : mux_generate.v
Verilog Code :

![mux1](https://github.com/user-attachments/assets/4cd13039-dc42-488f-b560-228e8eef6a7c)


Simulated Output Waveform :

![mux2](https://github.com/user-attachments/assets/961dcab2-8e30-4388-8d51-2208967bb5ca)


Synthesized Circuit :

![mux3](https://github.com/user-attachments/assets/755d8b0c-892a-41e7-9dc9-e6ca6904806e)



#### Design 2 : demux_case.v
Verilog Code :

![demux_case1](https://github.com/user-attachments/assets/fea575b9-7a22-4c70-832b-78190006204c)


Simulated Output Waveform :

![demux_case2](https://github.com/user-attachments/assets/61b2b87d-dd32-4817-954a-9380b37b1555)


Synthesized Circuit :


![demux_case3](https://github.com/user-attachments/assets/eab1b40e-3cb7-4c96-b8ee-2cf7828c1066)



#### Circuit 3 : demux_generate.v
Verilog Code :

![demux_generate1](https://github.com/user-attachments/assets/774a6f36-8fbc-454b-b07c-799dd1f8b90b)


Simulated Output Waveform :

![demux_generate2](https://github.com/user-attachments/assets/15d18fbe-1279-4be8-8cb5-e8823cc96906)


Synthesized Circuit :

![demux_generate3](https://github.com/user-attachments/assets/5d8b26f0-e449-4944-88b0-0968846c1e17)




# 
#  
# 


#### Circuit 4 : rca.v (Ripple Carry Adder)
In this verilog module, 'for generate' loop is used.

Verilog Code :
rca.v

![rca](https://github.com/user-attachments/assets/0c7d071e-726f-4839-b283-b83253994df9)


fa.v


![fa](https://github.com/user-attachments/assets/3447a9f3-08e4-4094-981d-0f8cd29e0684)


RTL Simulated Output Waveform :


![rca2](https://github.com/user-attachments/assets/0128c1b5-460b-4cb4-a976-65869d4bc91d)



Synthesized Circuit :


![rca3](https://github.com/user-attachments/assets/534175dd-d4ea-44c3-94f2-f92662d5d65c)


Flattened Synthesized Circuit :


![rca_flat](https://github.com/user-attachments/assets/d667fcf5-5555-4e99-a34f-ea2d492651c7)


Gate Level Simulation (GLS) Output Waveform :


![rca_gls](https://github.com/user-attachments/assets/c7bd36ed-dfcd-48bf-83c2-0c9b999a457f)






