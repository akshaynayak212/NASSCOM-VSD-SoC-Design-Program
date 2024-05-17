# NASSCOM-VSD-SoC-Design-Program
Exploring the ASIC design flow using tools like Openlane and the Google-Sky Water collaboration's 130nm process design kit (PDK). Led by industry leader Kunal Ghosh, this course equips with the skills to craft standard cells, navigate the Physical Design domain, and generate GDSII files.


Hello everyone! I'll be sharing what I've learned from a 5-day workshop on VLSI-SOC and design.
<br>

#### <b>Note :</b> <i>All the blockdiagrams and flow diagrams included in this repository are sourced from the VLSI System Design's SoC Design course.</i>
[VLSI SYSTEM DESIGN (VSD)](https://www.vlsisystemdesign.com/)
## Table of contents :
    - DAY-1 : - INTRODUCTION 
              - OPENLANE AND STRIVE CHIPSETS

    - DAY-2 : - TOOL INVOCATION & OPERATION 
              - GETTING STARTED - SYNTHESIZING THE DESIGN
  
                  








## DAY 1 : 

### INTRODUCTION

####  <li> Introduction to QFN-48 Package, chip, pads, core, die and IPs </li>

   - Learned how VLSI technology packs tons of tiny transistors onto chips, making electronics faster, smaller, and cheaper.

   - Looked at an Arduino board to understand why its main 'chip' is a big deal.
   - Saw how this chip, known as the microcontroller unit (MCU), runs everything on the board, like reading sensors and controlling lights.
   - Noticed how VLSI tech helps make these chips, making gadgets like Arduinos possible.
   - The Arduino Microcontroller Board comprises various elements like the microprocessor, voltage regulator, I/O pins, and communication interfaces. The microprocessor, highlighted , acts as the brain, executing instructions and managing the board's functions. The below provided image shows an Arduino Microcontroller Board, with a specific focus on the Microprocessor (chip). 

 
 <li> Chip Packaging and Components </li>
 <br>
- The places that make chips, called <b>'FOUNDRY'</b>, are really important for how well chips work.
<br>
- <b>'MACROS'</b> are digital parts inside chips that make them work better.

<br>

 <br>
 
![components (2)](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/eaeac9c5-ca55-4910-b356-49922e088547)

 There are three main components ,they are:
 
1) <b>Core</b>: Refers to the region where our complete logic will be implemented.

2) <b>Pads</b>:Through pads signals travel from external sources to chip or vice-versa.

3) <b>Die</b>: Refers to the entire area of the chip.

   ![components (1)](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/fa09ff1c-d118-45dc-84b9-68214bddaa6f)

<br>

<li><b>Introduction to RISC-V </li></b>
<br>
    
**ISA (Instruction Set Architecture)**: ISA helps software talk to hardware. When we write code in languages like C or Java, computers need a special language called machine code. ISA translates our code into machine code so computers can understand it. RISC-V is the latest version of this translator.

<br>

**From Software to Hardware**:

In everyday use, we use apps to work with hardware. System software helps apps talk to hardware. This happens in a few steps:

**Operating System (OS)**: The OS handles tasks like managing files and memory. It turns app code into a language that a hardware can understand.

**Compiler**: The compiler turns this language into instructions for the hardware  i.e .exe file

**Assembler**: The assembler turns these instructions into the binary coded language by which hardware does the operations.
<br>

**<li>Components of open-source digital asic design </li>**
<br>
![WhatsApp Image 2024-05-17 at 5 27 31 PM](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/1bd13b83-370d-4cd0-bb20-1fee9153c474)
<br>

To design a Open Source Digital ASIC, Components are :

**(1) RTL Designs**

**(2) EDA Tools**

**(3) PDK Data**

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

![WhatsApp Image 2024-05-17 at 8 33 23 PM](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/c4e5b99c-0109-45db-b56f-25274c4d4804)

<br>

**<li>OpenLANE ASIC design flow</li>**

<br>

![WhatsApp Image 2024-05-17 at 8 31 48 PM](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/f94a13ab-6cbe-4735-b360-619977aa5fd0)

</ul>

## DAY - 2 : 

### TOOL INVOCATION & OPERATION:

- We're using the Sky130_fd_sc_hd PDK variant.
- "Sky130" refers to the process or node name.
- "fd" indicates the foundry name, which is SkyWater foundry.
- "sc" denotes standard cell library files.
- "hd" represents high density, a specific variant.
- The Sky130_fd_sc_hd variant includes various technology files such as Verilog, Spice, Techlef, Meglef, Mag, GDS, CDL, LIB, LEF, etc.
- The techlef file provides layer information essential for the design process.

  <br>

<ul>
    
**<li>Directory order to invoke the tool OPENLANE </li>**

**Desktop/work/tools/openlane_working_dir/openlane**

In order to enter into BASH in terminal ,we must use a command **docker**. 

Now enter the follwing commands to invoke the openlane in terminal i.e using bash programming:

-bash-4.2$ **pwd** <br>
/OpenLANE_flow <br>
-ls -ltr ( it includes several files like flow.tcl,scripts,conf.py files,README files  nearly 136 files etc) as shown in below image
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

next commands :  - **cd designs**
                 - **cd picorv32a**
                 - **ls -ltr**

**picorv32a** contains files like config.tcl,sky130 tcl files,src, and new directory **runs** as been created by design setup asshown in below image
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

Now we need to perform  the Synthesis process on the design. command used is **run_synthesis**.
<br>
![Screenshot from 2024-05-16 22-07-55](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/27561569-d3c9-4abd-8311-6288d7f01e15)


<br>



It'll take a while (1-2 min) to perform synthesis but once it's done,we will see a message saying **'Synthesis completed successfully'**.
<br>
![Screenshot from 2024-05-16 22-09-52](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/2651d395-74a3-4aca-b964-aeb1106d1efb)

<br>


<li>Characterization of the synthesis results  </li>

















    
</ul>
