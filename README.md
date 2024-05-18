# NASSCOM-VSD-SoC-Design-Program
Exploring the ASIC design flow using tools like Openlane and the Google-Sky Water collaboration's 130nm process design kit (PDK). Led by industry leader Kunal Ghosh, this course equips with the skills to craft standard cells, navigate the Physical Design domain, and generate GDSII files.


Hello everyone! I'll be sharing what I've learned from a 5-day workshop on VLSI-SOC and design.
<br>

#### <b>Note :</b> <i>All the blockdiagrams and flow diagrams included in this repository are sourced from the VLSI System Design's SoC Design course.</i>
[VLSI SYSTEM DESIGN (VSD)](https://www.vlsisystemdesign.com/)
## Table of contents :
    - DAY-1 : - INTRODUCTION 
              - OPENLANE AND STRIVE CHIPSETS
              - COMMANDS USED IN OpenLANE FLOW
              - TOOL INVOCATION & OPERATION 
              - GETTING STARTED - SYNTHESIZING THE DESIGN

    - DAY-2 : - CHIP FLOOR PLANNING CONSIDERATION 
              - STEPS TO RUN FLOORPLAN & REVIEW FLOORPLAN FILES 
              - CONGESTION AWARE PLACEMENT USING REPLACE 
                  








## DAY 1 : 

### INTRODUCTION

In the DAY 1 lecture series 

   - Learned how VLSI technology packs tons of tiny transistors onto chips, making electronics faster, smaller, and cheaper.

   - Looked at an Arduino board to understand why its main 'chip' is a big deal.
   - Saw how this chip, known as the microcontroller unit (MCU), runs everything on the board, like reading sensors and controlling lights.
   - Noticed how VLSI tech helps make these chips, making gadgets like Arduinos possible.
   - The Arduino Microcontroller Board comprises various elements like the microprocessor, voltage regulator, I/O pins, and communication interfaces. The microprocessor, highlighted , acts as the brain, executing instructions and managing the board's functions. 
 
 <li> Chip Packaging and Components </li>
 <br>
- The places that make chips, called <b>'FOUNDRY'</b>, are really important for how well chips work.
<br>
- <b>'MACROS'</b> are digital parts inside chips that make them work better.

<br>

 There are three main components ,they are:
 
1) <b>Core</b>: Refers to the region where our complete logic will be implemented.

2) <b>Pads</b>:Through pads signals travel from external sources to chip or vice-versa.

3) <b>Die</b>: Refers to the entire area of the chip.

   ![components (1)](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/fa09ff1c-d118-45dc-84b9-68214bddaa6f)

<br>


**<li>Components of open-source digital asic design </li>**
<br>
![WhatsApp Image 2024-05-17 at 5 27 31 PM](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/1bd13b83-370d-4cd0-bb20-1fee9153c474)
<br>

Process Design Kit is PDK data which contains information about the manufacturing process. In 2020, Google collaborated with **SkyWater Technology** to release an **open-source FOSS 130nm** Production PDK.

**<li>RTL2GDS Flow</li>**

![WhatsApp Image 2024-05-17 at 5 27 32 PM](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/4316462c-f36c-44a2-a9d9-406bd5c7a295)

<br>

Above shows simplified RTL to GDSII flow.Steps invloved are explained as follows:

**Step 1 - Synthesis:** -In thi stage RTL is converted to gate level netlist using components from the Standard Cell Library(SCL). These components, known as Standard Cells, have regular layouts with varying widths.

**Step 2 - Floor Planning & Power Planning: :** In floor planning, we decide where to put components on the chip to make it as small as possible. We also plan where to put inputs, outputs, dimensions and power connections.

In power planning, the power supply network (VDD & GND) using special components of chip will be laid out.  

**step 3 - Placement:**

During placement, we put components and standard cells in their designated spots on the chip. We do this in two steps: first Global Placement, then Detailed Placement.

**step 4 - CTS (Clock Tree Synthesis):**

Before connecting signals, we organize the clock signals to avoid timing issues. We use special structures to make sure the clock arrives at different parts of the chip at the same time.

**step 5 - Routing:**

Once the clock is set up, we connect the rest of the signals. We use the remaining metal layers to make these connections. First, we plan out the routes (Global Routing), then we actually make the connections (Detailed Routing).

**step 6 - Sign-off:**

Finally, we check if everything is correct. We make sure the design follows the rules (Design Rule Check - DRC), matches the plan (Layout Vs. Schematic - LVS), and meets timing requirements (Static Timing Analysis - STA).


## OPENLANE AND STRIVE CHIPSETS

OpenLane began as an open-source project aiming to facilitate a genuine open-source tape-out experiment. It originated from e-fabless and serves as a platform that incorporates various tools like **Yosys, OpenRoad, Magic, KLlayout**, and other open-source tools. OpenLane streamlines the different stages of silicon implementation, making them easier to understand and work with. At e-fabless, they have a series of SOC (System on Chip) designs called Strive. Strive SOCs are entirely open, featuring open PDK (Process Design Kit), open RTL (Register Transfer Level), and open EDA (Electronic Design Automation) tools.

The Main aim of Openlane is to **produce clean GDSII without human intervention.**

<br>

**<li>OpenLANE ASIC design flow</li>**

<br>

![WhatsApp Image 2024-05-17 at 8 31 48 PM](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/f94a13ab-6cbe-4735-b360-619977aa5fd0)

</ul>
<br>

### COMMANDS USED IN OpenLANE FLOW:


1. prep -design <design> -tag <tag> -config <config> -init_design_config -overwrite
2. run_synthesis
3. run_floorplan
4. run_placement
5. run_cts
6. run_routing
7. run_magic
8. run_magic
9. run_magic_spice_export
10. run_magic_drc
11. run_netgen
12. run_magic_antenna_check

for fully automated run we can use command : **./flow.tcl -deisgn picorv32a**


### TOOL INVOCATION & OPERATION:

- We're using the Sky130_fd_sc_hd PDK variant.
- "Sky130" refers to the process or node name.
- "fd" indicates the foundry name, which is SkyWater foundry.
- "sc" denotes standard cell library files.
- "hd" represents high density, a specific variant.
- The Sky130_fd_sc_hd variant includes various technology files such as Verilog, Spice, Techlef, Meglef, Mag, GDS, CDL, LIB, LEF, etc.
- The techlef file provides layer information essential for the design process.

  <br>

<ul


    
**<li>Directory order to invoke the tool OPENLANE </li>**

**Desktop/work/tools/openlane_working_dir/openlane**

In order to enter into BASH in terminal ,we must use a command **docker**. 

Now enter the follwing commands to invoke the openlane in terminal i.e using bash programming:

-bash-4.2$ **pwd** <br>
/OpenLANE_flow <br>
**-ls -ltr** ( it includes several files like flow.tcl,scripts,conf.py files,README files  nearly 136 files etc) as shown in below image
<br>

![Screenshot from 2024-05-16 21-51-13](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/114d3965-cc2a-49a9-b24b-a77625918828)

<br>

next enter the command **./flow.tcl -interactive**  ,  Now OpenLane tool is opened & invoked as shown in below image. next is to input the required package by command **pacakage require openlane 0.9**
<br>

![Screenshot from 2024-05-16 21-51-25](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/67f0dac5-66a8-4b1e-b52b-f44b000b432d)
<br>

**<li>Design Preparation Setup</li>**

We will be designing Picorv32a CPU.this is basically a design setup stage where merging of two LEF's files is done i.e cell level LEF and Technology level LEF 

commands is as follows:

**prep -design picorv32a**

<br>

![Screenshot from 2024-05-16 21-51-50](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/9a9f3a3d-cd47-4f99-b821-b1a2e94da9c8)

<br>

next commands :  - **cd designs**<br>
                 - **cd picorv32a**<br>
                 - **ls -ltr**<br>

**picorv32a** contains files like config.tcl,sky130 tcl files,src, and new directory **runs** as been created by design setup as shown in below image
<br>
![Screenshot from 2024-05-16 22-04-18](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/edede503-cb1c-4c86-a98c-ebf498e0a890)
<br>

newly created **runs** folder in picorv32a directory includes the date on which we did design setup for ex : in my case its **16-05_16-20** as shown in below image
<br>

![Screenshot from 2024-05-16 22-05-11](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/846be161-3489-4919-89e6-f6a8fcebea2d)
<br>

next command - **cd date created** for ex: in my case its **cd 16-05_16-20** it includes tmp,results,logs,config.tcl files extra
<br>
![Screenshot from 2024-05-16 22-05-43](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/c3dc1007-1d11-4cd9-b2cc-42bc994f3dac)
<br>

### GETTING STARTED - SYNTHESIZING THE DESIGN :

Next step is we need to perform the Synthesis process on the design. command used is **run_synthesis**.
<br>
![Screenshot from 2024-05-16 22-07-55](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/27561569-d3c9-4abd-8311-6288d7f01e15)


<br>



It'll take a while (1-2 min) to perform synthesis but once it's done,we will see a message saying **'Synthesis was successful'**.
<br>
![Screenshot from 2024-05-16 22-09-52](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/2651d395-74a3-4aca-b964-aeb1106d1efb)

<br>


**<li>Characterization of the synthesis results  </li>**
<br>

![Screenshot from 2024-05-18 00-11-19](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/3b627411-b7c4-47e0-8431-1cff9ba2bb84)

<br>

From the  above image,data of synthesis obtainted , total number of counter D flip-flops is **1613** and the total number of cells is **18036**.
The flipflop percentage is obtained by formula i.e **Flop Ratio = ((no of D_flipflops) / (Total no of cells))100**
so we get Flop ratio =(1613/18036)*100 = **8.94 %.**

Before running, the result folder was empty. Now, after running synthesis, we can see that ABC has mapped everything in the reports folder.

<br>

![Screenshot from 2024-05-17 23-59-16](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/94329035-180c-4444-9273-d16e5a606c6e)

<br>
</ul>

### CHIP FLOOR PLANNING CONSIDERATION 

<ul>
    
**<li> UTILIZATION FACTOR AND ASPECT RATIO </li>**

In order to calculate the Utilization Factor and Aspect Ratio, we must know the height and width of core and die areas.
formula is given by:

**Utilization Factor = area occupied by the netlist / Total area occupied by the core**

--> If the utilization factor is 1 then it denotes 100 % utilization.
--> We never go for 100 % utilization, we go for 50 % or 60 % factor.

**Aspect Ratio = height of the core / width of the core**

--> When aspect ratio is 1 , then its a square chip.



### STEPS TO RUN FLOORPLAN & REVIEW FLOORPLAN FILES 

Once synthesis is sucessful,next step is floorplan. we use command **run_floorplan**
<br>
![Screenshot from 2024-05-16 22-16-03](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/7ace1039-925a-4a31-8e4d-09aa00d815a0)
<br>

This will create a folder inside **runs** folder of **picorv32a** directory.
it will take a while to execute.once done we will get **PDN GENERATION IS SUCESSFUL** as shown in below image.
<br>
![Screenshot from 2024-05-16 22-16-43](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/804cb295-a0af-49c8-b09f-9917d9dd50ab)
<br>

Next step is to view the **VMetal and HMetal** (vertical metal & horizontal metal) , this will be available in **config.tcl** of the newly created folder of floorplan in date's folder in runs directoy
<br>

<br>

now go to tmp folder from date created folder ,use this command

**openlane/designs/picorv32a/runs/16-05_16-20/tmp/floorplan**

use command **ls -ltr** def files are available as shown in below image.
<br>

![Screenshot from 2024-05-16 22-22-49](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/114478f0-b073-4a30-8c2a-8480149e8ccb)
<br>



if we open this file, we can see all information about die area ,database units. def file is **4-ioPlacer.def** open this file using command **less 4-ioPlacer.def** we can see the die area, unit distance in micron.,unit distance in micron (1000), Die area  is (0 0) (660685 671405). it means 1 micron means 1000 databased units. so 660685 and 671405 are databased units. and if we devide this by 1000 then we can get the dimensions of chips in micrometer.

<br>

![Screenshot from 2024-05-16 22-22-52](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/e4ac953f-3843-4189-815b-d21a0422cc44)

<br>























    
</ul>
