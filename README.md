# NASSCOM-VSD-SoC-Design-Program
Exploring the ASIC design flow using tools like Openlane and the Google-Sky Water collaboration's 130nm process design kit (PDK). Led by industry leader Kunal Ghosh, this course equips with the skills to craft standard cells, navigate the Physical Design domain, and generate GDSII files.


Hello everyone! I'll be sharing what I've learned from a 5-day workshop on VLSI-SOC and design.
<br>

#### <b>Note :</b> <i>All the images included in this repository are sourced from the VLSI System Design's SoC Design course.</i>
[VLSI SYSTEM DESIGN (VSD)](https://www.vlsisystemdesign.com/)
## Table of contents :
    - DAY-1 : - INTRODUCTION 
              - OPENLANE AND STRIVE CHIPSETS
  
                  








## DAY 1 : 

### INTRODUCTION

####  <li> Introduction to QFN-48 Package, chip, pads, core, die and IPs </li>

 <b> Arduino Board: </b> The Arduino Microcontroller Board comprises various elements like the microprocessor, voltage regulator, I/O pins, and communication interfaces. The microprocessor, highlighted , acts as the brain, executing instructions and managing the board's functions. The below provided image shows an Arduino Microcontroller Board, with a specific focus on the Microprocessor (chip). 
 
 ![Screenshot (76)](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/68003ba1-02c2-47d7-b254-c2f73ac0dad8)

 
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

**Step 1 - Synthesis:** -In thi stage RTL is converted to gate level netlist using components from the Standard Cell Library. These components, known as Standard Cells, have regular layouts with varying widths.

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







</ul>
