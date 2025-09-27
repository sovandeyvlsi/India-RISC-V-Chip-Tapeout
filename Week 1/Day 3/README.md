
# India-RISC-V-Chip-Tapeout-Week1

## Day 3 :
### Lab-6 : Combinational Logic Optimisations

Here, we do the synthesis of some Combinational circuit with logic Optimisations.
We will follow the synthesis steps as mentioned in [Lab 3.](https://github.com/sovandeyvlsi/India-RISC-V-Chip-Tapeout/tree/main/Week%201/Day%201#lab-3-d1sk4-l1--yosys-1-good-mux)

Here, aditionally we only add an optimization command in between *'synth -top design_file'* 

and

*'abc -liberty /path-of-lib-file/lib/sky130_fd_sc_hd__tt_025C_1v80.lib'* as :

    opt_clean -purge
### Circuit 1 : opt_check.v
Verilog Code :

![opt 00](https://github.com/user-attachments/assets/59a79165-6f66-4675-b5f2-d3534f555056)


Optimized Synthesized Circuit :

![opt 01](https://github.com/user-attachments/assets/2cae34cf-e128-4205-81b1-f8348a7eb8bd)



### Circuit 2 : opt_check2.v
Verilog Code :

![opt 20](https://github.com/user-attachments/assets/c3a7a314-4880-4d20-8e64-254d624fd562)


Optimized Synthesized Circuit :

![opt 21](https://github.com/user-attachments/assets/14141a01-3a58-437a-ae56-d8aced54e5d2)


### Circuit 3 : opt_check3.v
Verilog Code :

![opt 30](https://github.com/user-attachments/assets/b75300dd-9208-4ef7-84ce-74e7e5e6b891)


Optimized Synthesized Circuit :

![opt 31](https://github.com/user-attachments/assets/ebd51955-f34a-4367-a262-994ee33aacff)


### Circuit 4 : opt_check4.v
Verilog Code :

![opt 40](https://github.com/user-attachments/assets/a5627d9b-052e-4446-9554-bc97a5b4addf)


Optimized Synthesized Circuit :

![opt 41](https://github.com/user-attachments/assets/2f695c28-3776-4f96-b441-0668505cccda)



### Circuit 5 : multiple_module_opt.v
Verilog Code :

![opt mul 00](https://github.com/user-attachments/assets/bd2642c8-d998-4708-be89-d03f377c0cb3)


Optimized Synthesized Circuit :

![opt mul 01](https://github.com/user-attachments/assets/6e26f9db-922f-44d0-9d63-ee54a1dbb39a)


Synthesized Circuit of sub_module1 :

![opt mul 02](https://github.com/user-attachments/assets/83abcf75-a533-42c8-8a35-cf6fc8cd59c6)


### Circuit 6 : multiple_module_opt2.v
Verilog Code :

![opt mul 20](https://github.com/user-attachments/assets/a0a77a83-3dee-4333-bf04-c583efd70e75)


Optimized Synthesized Circuit :

![opt mul 21](https://github.com/user-attachments/assets/44306d16-aa95-42e0-a6c7-d4035fa4a55d)


Synthesized Circuit of sub_module :

![opt mul 22](https://github.com/user-attachments/assets/1f209b23-3e58-4a51-a2a9-3f0f6f7cb338)











### Lab-7 : Sequential Logic Optimisations

Here, we do the simulations and optimized synthesis of some Combinational circuits.
We will follow the simulation steps mentioned in [Lab 2](https://github.com/sovandeyvlsi/India-RISC-V-Chip-Tapeout/tree/main/Week%201/Day%201#lab-2-d1sk2-l2-lab2--introduction-to-iverilog-gtkwave-part-1) and also follow the synthesis steps as mentioned in [Lab 3.](https://github.com/sovandeyvlsi/India-RISC-V-Chip-Tapeout/tree/main/Week%201/Day%201#lab-3-d1sk4-l1--yosys-1-good-mux)

Here, in the synthesis steps, we add an aditional step of D Flipflop library mapping after the *"synth - top design_file"* as :

    dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

### Circuit 1 : dff_const1.v
Verilog Code :

![dff11](https://github.com/user-attachments/assets/5dfcd05c-9a65-4a33-9f1c-0608b5f38629)


Simulated Output Waveform :

![dff12](https://github.com/user-attachments/assets/54f256a2-737f-40fd-9208-7e1519910261)


Synthesized Circuit :


![dff13](https://github.com/user-attachments/assets/fed7373f-f32f-42e0-acf3-d670c587eeab)



### Circuit 2 : dff_const2.v
Verilog Code :

![dff21](https://github.com/user-attachments/assets/2272d7f3-ffcb-4cf9-9c52-376ecf653abd)


Simulated Output Waveform :

![dff22](https://github.com/user-attachments/assets/0a9627ad-738b-451d-8385-7d8c35c32f80)



Synthesized Circuit :

![dff23](https://github.com/user-attachments/assets/26fb0a62-cae1-43fb-acbe-5dc5da34800a)


### Circuit 3 : dff_const3.v
Verilog Code :

![dff31](https://github.com/user-attachments/assets/35d3459f-16c5-45b9-957d-1107bd120a9d)


Simulated Output Waveform :

![dff32](https://github.com/user-attachments/assets/f148cd25-9534-4ee3-88e0-f53812231413)


Synthesized Circuit :

![dff33](https://github.com/user-attachments/assets/45a6af71-f486-4a73-8511-78f9d68e1593)


### Circuit 4 : dff_const4.v
Verilog Code :

![dff41](https://github.com/user-attachments/assets/c0670792-c214-4a42-a099-b93556ee7782)


Simulated Output Waveform :

![dff42](https://github.com/user-attachments/assets/6ca280c0-7bbb-477b-87a6-2113bcdb9dd3)


Synthesized Circuit :


![dff43](https://github.com/user-attachments/assets/2fee24f6-9571-47f4-ab28-a122bad56fde)



### Circuit 5 : dff_const5.v
Verilog Code :

![dff51](https://github.com/user-attachments/assets/c5a02924-59e1-4823-a01a-11038a42d681)


Simulated Output Waveform :


![dff52](https://github.com/user-attachments/assets/d6684c4a-ff26-43ec-b2e7-ec5332e3c5fd)


Synthesized Circuit :

![dff53](https://github.com/user-attachments/assets/09f449e4-e640-4fef-b599-6a447ba04005)









