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






