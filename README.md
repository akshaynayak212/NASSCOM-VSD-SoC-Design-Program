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
              - STEPS TO RUN PLACEMENT
              
    - DAY-3 : - DESIGN LIBRARY CELL DESIGN USING MAGIC AND NGSPICE CHARACTERIZATION 
                 - Steps to create std cell layout and extraction of spice netlist
                 - Opening of layout of cmos inverter using magic tool
                 - Extraction of spice netlist
                 - Transient analysis & steps to characterize the Inverter
              - INTRODUCTION TO MAGIC TOOL AND STEPS TO LOAD SKY130 TECH - RULES 

    - DAY-4 : - PRELAYOUT TIMING ANALYSIS AND CLOCK TREE SYNTHESIS 
              - Steps to convert magic layout to std cell LEF
              - Steps to configure synthesis settings to fix slack
              - TIMING ANALYSIS USING openSTA
              - INTRODUCTION TO MAGIC TOOL AND STEPS TO LOAD SKY130 TECH - RULES 
              - Post-CTS OpenROAD timing analysis


    - DAY -5 : - Final step for RTL2GDS using tritinRoute and openSTA
               -

    - Acknowledgement

              








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

```
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

for fully automated run we can use command : ./flow.tcl -deisgn picorv32a
```


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
```
Desktop/work/tools/openlane_working_dir/openlane
```

In order to enter into BASH in terminal ,we must use a command 
```
docker
```

Now enter the follwing commands to invoke the openlane in terminal i.e using bash programming:

```
-bash-4.2$ pwd
/OpenLANE_flow 
-ls -ltr ( it includes several files like flow.tcl,scripts,conf.py files,README files  nearly 136 files etc) as shown in below image

```

![Screenshot from 2024-05-16 21-51-13](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/114d3965-cc2a-49a9-b24b-a77625918828)

<br>

next enter the command 
```
./flow.tcl -interactive
```
Now OpenLane tool is opened & invoked as shown in below image. next is to input the required package by command **pacakage require openlane 0.9**
<br>

![Screenshot from 2024-05-16 21-51-25](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/67f0dac5-66a8-4b1e-b52b-f44b000b432d)
<br>

**<li>Design Preparation Setup</li>**

We will be designing Picorv32a CPU.this is basically a design setup stage where merging of two LEF's files is done i.e cell level LEF and Technology level LEF 

commands is as follows:
```
prep -design picorv32a
```

<br>

![Screenshot from 2024-05-16 21-51-50](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/9a9f3a3d-cd47-4f99-b821-b1a2e94da9c8)

<br>

next commands :  
```
cd designs
cd picorv32a 
ls -ltr 
```

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

Next step is we need to perform the Synthesis process on the design. command used is

```
run_synthesis
```


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

Once synthesis is sucessful,next step is floorplan. we use command 
```
run_floorplan
```

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

![Screenshot from 2024-05-18 13-15-43](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/7a065019-0bea-4ee3-95fd-e00984747ae2)

<br>

now go to tmp folder from date created folder ,use this command
```
openlane/designs/picorv32a/runs/16-05_16-20/tmp/floorplan

```
<br>

use command 
```
ls -ltr 
```

def files are available as shown in below image.
<br>

![Screenshot from 2024-05-16 22-22-49](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/114478f0-b073-4a30-8c2a-8480149e8ccb)

<br>




we are interested in def file called **4-ioPlacer.def** open this file using command 

```
less 4-ioPlacer.def
```


we can see the die area, unit distance in micron.,unit distance in micron (1000), Die area  is (0 0) (660685 671405).660685 and 671405 are databased units. and if we divide this by 1000 (unit distance)  then we can get the dimensions of chips in micrometer.therefore the width of chip is 660.685 micrometer and height is 671.405 micrometer.

<br>

![Screenshot from 2024-05-16 22-22-52](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/e4ac953f-3843-4189-815b-d21a0422cc44)

<br>


To see the actual layout after the floorplan ,go the folders as shown below:
```
openlane/designs/picorv32a/runs/16-05_16-20/results/floorplan
```

now we need to open the **magic** file by the  following command
<br>

```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```



<br>

![Screenshot from 2024-05-16 22-35-15](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/9376ac56-c91e-4524-ab17-7d254282aa13)
<br>
we will get the layout as shown in below image
<br>Pre-layout timing analysis and clock tree synthesis

![Screenshot from 2024-05-16 22-36-41](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/33a052a0-f11a-4dab-8b66-dda975fbcc3c)
<br>
To zoom in press left button of mouse then right button and press z 
<br>
![Screenshot from 2024-05-16 22-38-02](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/5e7db0d4-169e-4faf-ba66-ddf3a5f50b6e)
<br>

In order to know the details of any cell in the layout , just move the cursor to that cell and press **S** to select the cell and then in the window of **tkcon** enter the command **"what"**. then it will displey the details of the selected cell.
lets see the detail of horizontal and vertical pins , in tkcon window it shows that the pin is in the metal 3 for horizontal pins ,similarly for the vertical pins, we see that thepin is at metal 2. image is shown below.
<br>
![Screenshot from 2024-05-16 22-40-09](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/e492e6b9-223c-4ae8-94f0-c2c774ff56f4)
![Screenshot from 2024-05-16 22-40-20](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/f4cfea60-a78e-479a-ad9b-da645c1b3311)


<br>

![Screenshot from 2024-05-16 22-42-19](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/cc2a9a61-fe67-44a8-bed4-f7f7467676d5)
![Screenshot from 2024-05-16 22-42-35](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/da1fd5a6-6a93-4f68-af1f-280602bc6f0d)

<br>
</ul>


### STEPS TO RUN PLACEMENT

Once the Floorplanning is done sucessfully , the next step in the process is Placement. 
To run the placement use the command
```
run_placement
```
<br>

![Screenshot from 2024-05-17 09-22-55](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/5e59922a-9493-45d7-b4c1-f71c0b4eb2cc)

<br>

It will take few seconds. once done it shows **Placement done sucessfully**

<br>

![Screenshot from 2024-05-17 09-36-03](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/dec8479e-9890-4e03-a4fc-b86840239c27)
<br>

Once Placement process is done , next step is to check whether the cells are placed correctly or not.by using **magic** tool.

use the below command to view the standerd cells placement. image is shown below
```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

```
<br>

![Screenshot from 2024-05-17 10-04-35](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/0a8875be-cf67-428f-b654-f4719b12c44b)

![Screenshot from 2024-05-17 10-04-44](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/3111e1b6-63f4-4f73-93f9-a2f4d795aac9)

<br>


Zooom in (to zoom press z), we can see that the standard cells are all placed like gates,buffers, flip flops etc as shown in below image
<br>

![Screenshot from 2024-05-17 10-10-05](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/b0cec0e9-19c5-4916-a758-31a092a9807f)

<br>


### DESIGN LIBRARY CELL DESIGN USING MAGIC AND NGSPICE CHARACTERIZATION

<ul>

**<li>Steps to create std cell layout and extraction of spice netlist</li>**
<br>
First step is to gitclone the given files from github to **openlane** folder by below command:
```
 git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```
<br>

![Screenshot from 2024-05-20 21-09-42](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/27d46612-ff60-4f4b-a682-668c74f9aea2)
<br>
A new folder will be created in openlane directory as **vsdstdcelldesign** as shown in below image
<br>

![Screenshot from 2024-05-20 21-10-48](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/ccb8d4f9-fa07-4533-9f46-3f655f40680a)
<br>

Next step to copy the **sky130A.tech** file of magic from pdks folder to **vsdstdcelldesign** folder 

below given is the path from where **sky130A.tech** is to be copied to **vsdstdcelldesign** folder
```
home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech
```

**<li>Opening of layout of cmos inverter using magic tool</li>**

to open the layout of inverter working directory command is given  below

```
home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
```
<br>

next is to open the inverter design in the magic by below given command\
```
magic -T sky130A.tech sky130_inv.mag
```
<br>

![Screenshot from 2024-05-20 12-31-05](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/ec901e2b-ac7d-4af1-8d1f-750e929a1acc)

<br>

To check that whether CMOS inverter is working or not. we can check pmos,nmos,poly ,diffusion layer etc and other layers are arranged & connected properly or not by clicking on that area and press s and type **what** in tkon window ( another window other than layout window)

<br>

![Screenshot from 2024-05-20 12-13-49](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/1496e44c-f0d5-4d39-b3ac-3fd80d9b3bca)

![Screenshot from 2024-05-20 12-15-25](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/0fc285f6-9a86-4cb7-85fc-353d2c88761e)
<br>

**<li> Extraction of spice netlist </li>**

we need to write following commands in tkon window
```
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```
<br>

![Screenshot from 2024-05-20 12-30-42](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/b3577685-081b-4103-8cca-de3e0e9726e6)
<br>

now the spice model is generated , can be checked by using command ``` ls -ltr ``` in vsdstdcelldesign folder **sky130_inv.spice** is generated as shown in below image

<br>

![Screenshot from 2024-05-17 14-50-00](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/ceeffe2a-7ef2-424d-85cb-3eaa9f136cb9)

<br>

Once the extracting the SPICE file is done , next step is to update it according to the design of inverter.
use the below command
```
gedit sky130_inv.spice
```

we will get this window
<br>

![Screenshot from 2024-05-20 12-31-32](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/85e4cf31-47b5-4d92-a810-093516edf94c)


change  the following in SPICE file 

--> include pshort nshort library files
--> define VDD and VSS sources
--> create a pulse signal to create transient analysis.
as shown in below image:
<br>

![Screenshot from 2024-05-21 00-16-58](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/de34ba01-057c-4e3c-ab28-fa2227735b85)

<br>
<br>

**<li> Transient analysis & steps to characterize the Inverter </li>**
once we update the spice model , save and we need to run spice model using ngspice tool by command
```
ngspice sky130_inv.spice
```
<br>

![Screenshot from 2024-05-21 00-08-36](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/1f07c48c-c7be-4295-bcdb-5c635c6d075d)

<br>
we will get ngspice terminal to plot graph type command 

```
plot Y vs time a
```

<br>

![Screenshot from 2024-05-21 01-49-51](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/18dd66b7-6cbb-48ab-8b9e-015bc9a86ed0)

<br>

Transient analysis of cmos inverter image is given below
<br>

![Screenshot from 2024-05-21 00-18-15](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/6af7e41e-14a4-4780-b427-6beaeceb92b2)
<br>

next step is to calculate the rise time , fall time , cell rise delay and cell fall delay:
click on the waveforms to get values i.e 

--> 20 % of VDD (3.3 V) is 0.66V
--> 80 % of VDD (3.3 V) is 2.64V
--> 50 % of VDD (3.3 V) is 1.65V
<br>
1) **Rise time**- Time taken to the output waveform to 20% value to 80% value.

<br>

![WhatsApp Image 2024-05-21 at 1 56 45 AM(1)](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/e6be18ed-736a-4df4-ae12-a09afac58937)

<br>
therfore rise time= (2.24 - 2.18)e-09 = 0.64e-09s
  
2) **Fall time**- Time taken to the output waveform to 80% value to 20% value.
<br>



<br>
therfore fall time = (2.17999 - 2.12)e-09 = 0.5999e-09s


5) **cell rise delay**-Time difference between the 50% value of input and 50% value of the output.

<br>

![WhatsApp Image 2024-05-21 at 1 56 46 AM](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/f03945b9-f78b-46b8-bc39-af73de135a37)



<br>
therfore cell rise delay or propogation delay = (2.2107 - 2.1501)e-09 = 0.061e-09s

7) **cell fall delay**-Time difference between output falling to 50% and input is rising to 50% value.

<br>

![WhatsApp Image 2024-05-21 at 1 56 45 AM](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/04d2adf7-f47f-4d9f-830e-1f5f3ad379d0)


<br>
thefore cell fall delay = (4.077 -4.05)e-09 = 0.027e-09 s

</ul>

### INTRODUCTION TO MAGIC TOOL AND STEPS TO LOAD SKY130 TECH - RULES 
<ul>
First step is to download the lab files required for DRC error fixing by below coammand
    
```
   wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
```
to open magic use 
```
  magic -d XR
```
<br>

![Screenshot from 2024-05-21 02-21-56](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/30b370d7-7fe0-40ab-9d37-04e73d31f43a)
![Screenshot from 2024-05-21 02-22-56](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/c104bcc0-c5ac-4b3f-bbef-8dddae97f582)
![Screenshot from 2024-05-21 02-24-22](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/2134a46d-e12b-4e87-b87e-aa50e44aed91)

<br>


Open met met3.mag file from file -> Open in magic window

<br>

![Screenshot from 2024-05-21 02-28-23](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/981cce52-bfa1-4a4b-b97e-dcb17c62bd17)
<br
![Screenshot from 2024-05-21 02-29-44](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/d9b57b99-8bd0-41d5-87fd-3b9830e832ab)
<br>


![Screenshot from 2024-05-21 09-27-39](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/51b0d993-0c41-4d77-b664-6be93f8cea59)

![Screenshot from 2024-05-21 09-27-47](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/8de8ec48-cbb8-4b9c-954d-ed008e24c4f8)
![Screenshot from 2024-05-21 09-29-44](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/d684b929-e8b3-416d-919f-973400895a18)
<br>

There are some changes to be made in **sky130A.tech file**. Search for the **poly.9** in the **sky130A.tech** file. It appears in both the **POLY** and **uhrpoly** sections,changes given below:

open sky130A.tech file as shown below

<br>

![Screenshot from 2024-05-21 09-30-10](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/ed5c72ea-2148-40ad-b146-a8a769baa0e9)


<br>

![Screenshot from 2024-05-21 09-41-52](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/d29c9f03-29e7-4b1f-bb74-1611914c04e0)


<br>

![Screenshot from 2024-05-21 09-45-04](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/749cf951-eda5-46e4-937f-6ad00744ea70)

<br>

next step is to load the sky130A.tech file in tckon window as as shown below:
<br>
![Screenshot from 2024-05-21 09-45-35](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/3f281da7-04d7-456c-bbd7-8947901587ef)

<br>

DRC is checked as shown in below image:
<br>

![Screenshot from 2024-05-21 09-46-51](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/3a3afb3c-1bd6-428f-8fca-6af9c35358b5)

<br>
    
</ul>

## DAY-4 

### PRELAYOUT TIMING ANALYSIS AND CLOCK TREE SYNTHESIS 

<ul>
The next step is to get the **.lef** file from the inverter design.

Open the tracks.info file 
directory is : 
```
openlane_working_dir/pdk/sky130/libs.tech /openlane/sky130_fd_sc_hd/track.info 
```
<br>

![Screenshot from 2024-05-21 10-09-12](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/5c1350db-8bcb-4f85-9621-c07dc6d678ec)
<br>

Change grid into tracks in console window as shown in below image:

<br>

![Screenshot from 2024-05-21 10-12-26](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/6d6c8e36-9c3d-4034-8170-a9153f6d6025)

<br>

![Screenshot from 2024-05-21 10-12-43](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/7676e0e6-c2e6-40c6-8bd0-6311e6befaff)

<br>



**<li>Steps to convert magic layout to std cell LEF</li>**

for the extraction of lef file ,enter the given below command in the tckon window.

```
lef write
```

<br>

![Screenshot from 2024-05-21 10-14-12](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/d3002f17-2091-420d-8bf6-519caaddddd2)


<br>


now the **sky130_inv.lef** file is created in **vsdstdcelldesign** folder in **openlane** directory.

<br>

![Screenshot from 2024-05-21 10-14-54](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/c80b4f0b-77db-496e-8b9e-fe9c84b13071)



<br>

![Screenshot from 2024-05-21 10-15-09](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/b07b788d-2c87-4571-8e0b-7f2cc060bce4)
/bc2b3226-fc0a-4fda-a110-036a3f515eda)
<br>

The next step is to copy the newly created **.lef** file to src folder of **picorv32a** directory along with some important libraries.

libraries are present in following directory 
```
/openlane/vsdstdcelldesign/libs
```
<br>

![Screenshot from 2024-05-21 10-21-26](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/fb25c48c-d200-40ef-b6e3-6f9d9897b3f3)

<br>

![Screenshot from 2024-05-21 10-22-35](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/42f31410-0edb-487b-b67f-fa0acad3a870)
<br>

Now the next step is to edit the **config.tcl** of picorv32a design.

config.tcl file is present in **picorv32a** folder

<br>

<br>

NOW go to the openlane directory run **docker** command to go to bash terminal

next commands are given below:

```
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]      
add_lefs -src $lefs
run_synthesis
```
<br>

![Screenshot from 2024-05-21 11-55-42](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/2b4f0835-4ba4-40c9-b60b-43090f063153)

<br>

**<li> Steps to configure synthesis settings to fix slack </li>**

Once the synthesis is sucessfull, check the slack

<br>

![Screenshot from 2024-05-21 12-05-17](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/771dbeaa-89dd-422e-8944-32fd009f8559)

<br>

we get wns= -23.89  and tns== -711.5.

next command is to run floorplan

```
run_floorplan

```
if error occurs in floorplan stage use below commands one by one :
```
init_floorplan

place_io

tap_decap_or

```

next command is to run placement
```
run_placement

```
<br>

![Screenshot from 2024-05-21 12-10-59](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/323368c0-5e9f-4b8d-9802-3bf245301e01)

<br>

The standard cell inverter can be seen in the below image using magic tool

<br>

![Screenshot from 2024-05-21 12-16-14](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/f592c682-b208-4104-96a9-adce35b0e967)
<br>

![Screenshot from 2024-05-21 12-23-34](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/5e6d6b16-3647-4c15-b0e5-68aff7c7559b)

<br>

use the below command in tckon window to check whether inverter placed properly or not
```
expand
```
<br>

![Screenshot from 2024-05-21 12-24-58](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/60efee39-fa9d-4fea-bde4-a8be477a17d7)

<br>

![Screenshot from 2024-05-21 12-25-15](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/aa755300-e513-4a7a-b589-ee54ab8a99a5)
<br>

</ul>

### TIMING ANALYSIS USING openSTA

steps :

start with below commands :

```
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_SIZING) 1
run_synthesis


```

once synthesis is done create a **pre_sta.conf** file for in **openlane** directory
write the code as given in below image in **pre_sta.conf** file .

<br>

![Screenshot from 2024-05-21 13-28-44](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/01913529-11b8-4f96-9a3f-f556b352f940)



<br>

next create a **my_base.sdc** file in openlane/designs/picorv32a/src directory. 
write the code as given in below image in **my_base.sdc** file.

<br>

![Screenshot from 2024-05-21 13-36-57](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/cd9f4c03-3706-4240-a8b2-9187f6ef295b)
<br>

Now run sta in this openlane_working_dir/openlane  folder using the command :
```
sta pre_sta.conf
```

<br>

![Screenshot from 2024-05-21 13-37-31](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/07d91564-f4d0-49c9-9374-f889cf761a1f)

<br>

To check the connections to a net ,use the below command
```
report net -connenctions _10566_
```

Replace the cell with higher drive strength using this command
```

replace_cell _13165_ sky130_fd_sc_hd__or3_4
```

to check timing
```

report_checks -fields {net cap slew input_pins} -digits 4
```

### Clock tree synthesis TritonCTS and signal integrity

Steps to run CTS using TritonCTS :

Run the Synthesis , Floorplan and placement again

```
prep -design picorv32a -tag 05-05_10-43 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_STRATEGY) "DELAY 3"
set ::env(SYNTH_SIZING) 1
run_synthesis

init_floorplan
place_io
tap_decap_or

run_placement

```
To Run clocktree synthesis use below command :

```
run_cts
```

<br>

![Screenshot from 2024-05-21 16-43-53](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/26af6cad-31f8-486f-8bbe-644c73abfd93)

<br>

### Post-CTS OpenROAD timing analysis

use the below commands : (one by one)

```
openroad

read_lef /openLANE_flow/designs/picorv32a/runs/05-05_10-43/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/05-05_10-43/results/cts/picorv32a.cts.def
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/05-05_10-43/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

exit

```

<br>

![Screenshot from 2024-05-21 18-44-37](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/ee76fc61-0a82-4e4c-99fc-e278f96df4f1)

<br>




next commands :

```
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]
```


```
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/05-05_10-43/results/placement/picorv32a.placement.def
run_cts

```


<li> Enter the openROAD flow and check timing by using the following commands </li>

```
openroad
read_lef /openLANE_flow/designs/picorv32a/runs/05-05_10-43/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/05-05_10-43/results/cts/picorv32a.cts.def
write_db pico_cts1.db
read_db pico_cts1.db
read_verilog /openLANE_flow/designs/picorv32a/runs/05-05_10-43/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

exit

echo $::env(CTS_CLK_BUFFER_LIST)
set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]
echo $::env(CTS_CLK_BUFFER_LIST)


```
<br>

![Screenshot from 2024-05-21 19-40-43](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/acf1f028-2349-485e-8c25-5d7df41f787d)

<br>



## DAY 5 

###  Final step for RTL2GDS using tritinRoute and openSTA

first step is to build  the power distribution network by follwing command :
```
gen_pdn

```

<br>

![Screenshot from 2024-05-21 19-40-57](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/70e45772-1fd8-4c80-9b69-01ba47f701eb)

<br>

To check PDN, open Magic tool go to /tmp/floorplan/ indside the run folder in openlane directory by using below commands :

```

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &
```

<br>

![Screenshot from 2024-05-21 19-42-20](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/1f5f42ea-7eb2-4c9e-a1e9-fb3f8376b6f7)

<br>

![Screenshot from 2024-05-21 19-42-31](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/3d84ce66-7a3a-4bb9-9df4-336938086d8f)
<br>

Final steis routing . to run routing use below command :

```
run_routing
```

To view the final design  with routing in Magic tool , go to the results/routing/ in  the runs folder of openlane directory by using below command :

```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &

```

<br>

![Screenshot from 2024-05-21 20-29-57](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/f8a94db9-98e1-4d1a-982e-e497a8bd0e94)

<br>

![Screenshot from 2024-05-21 20-30-04](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/3c23184b-cb1b-4349-b6f8-27625e0536de)

<br>

![Screenshot from 2024-05-21 20-30-51](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/e7cf860e-25d8-418a-8821-d0482e645dbc)
<br>


## Acknowledgement


I want to give a big thank you to Mr. Kunal Ghosh, one of the founders of VLSI System Design (VSD) Corp. Pvt. Ltd., and Mr. Nickson Jose for their amazing help during the DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING workshop. They really know their stuff when it comes to chip design using OpenLANE software and other cool techniques. Their guidance has been super valuable in teaching me all about it.






















