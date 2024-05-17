# NASSCOM-VSD-SoC-Design-Program
Exploring the ASIC design flow using tools like Openlane and the Google-Sky Water collaboration's 130nm process design kit (PDK). Led by industry leader Kunal Ghosh, this course equips with the skills to craft standard cells, navigate the Physical Design domain, and generate GDSII files.

#### <b>Note :</b> <i>All the images included in this repository are sourced from the VLSI System Design's SoC Design course.</i>
[VLSI SYSTEM DESIGN (VSD)](https://www.vlsisystemdesign.com/)
## Table of contents :
    - DAY-1 : INTRODUCTION
        - 
                         








## DAY 1 : INTRODUCTION

####  <li> Introduction to QFN-48 Package, chip, pads, core, die and IPs </li>

 <b> Arduino Board: </b> The Arduino Microcontroller Board comprises various elements like the microprocessor, voltage regulator, I/O pins, and communication interfaces. The microprocessor, highlighted , acts as the brain, executing instructions and managing the board's functions. The below provided image shows an Arduino Microcontroller Board, with a specific focus on the Microprocessor (chip). 
 
 ![Screenshot (76)](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/68003ba1-02c2-47d7-b254-c2f73ac0dad8)

![chip](https://github.com/akshaynayak212/NASSCOM-VSD-SoC-Design-Program/assets/169296665/cd672f2a-d14b-4343-8e7c-c2ec1817d560)
<br>
 
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





</ul>
