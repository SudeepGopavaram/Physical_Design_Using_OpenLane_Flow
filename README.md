# Physical_Design_Using_OpenLane_Flow
This repository contains a detailed description of a RTL2GDSII flow using a opensource OpenLane flow, design used for this run is PicoRV32 which is a CPU core that implements the RISC-V Instruction Set.

# OpenLane
It is an automated RTL2GDSII flow which make use of several other opensource tools throughout the run to generate the GDSII like, OpenROAD, Yosys, Magic, Netgen, CVC, SPEF-Extractor, KLayout and other custom script for optimized flow.

**OpenLane Architecture**
![image](https://github.com/SudeepGopavaram/Physical_Design_Using_OpenLane_Flow/assets/57873021/818110cc-75b8-4540-b5cd-c25a20398606)

RTL2GDSII flow consist of various steps involved which help in converting Register Transfer Level(RTL) to a fabrication ready GDSII(Graphic Design System) format it is a industry standard for data exchange of IC layout.

* RTL Synthesis
* Static Timing Analysis(STA)
* Design for Testability(DFT)
* Floorplanning
* Placement
* Clock Tree Synthesis(CTS)
* Routing
* GDSII Streaming

This repository shows the detailed execution of all the above mentioned steps to complete the flow.

**Skywater Technology**
   
   ![image](https://github.com/SudeepGopavaram/Design_and_analysis_of_nmos_and_pmos_using_sky130pdk/assets/57873021/f8f19c5c-1ded-40c1-a87b-82dc2e572bab)

   The [SkyWater](https://www.skywatertechnology.com/technology-and-design-enablement/) Technology Foundry 130nm Process Design Kit (PDK) is a comprehensive collection of files, libraries, and documentation that enables the design and 
   fabrication of integrated circuits (ICs) using the SkyWater 130nm process technology.

   The SkyWater130 PDK is typically utilized in conjunction with electronic design automation (EDA) tools, enabling designers to create and verify their IC designs 
   within a familiar design environment. The PDK provides the necessary information for layout design, including design rules, layer information, and guidelines for 
   ensuring compatibility with the SkyWater 130nm process technology.

   Overall, the SkyWater130 PDK is an essential resource for IC designers seeking to leverage the capabilities of the SkyWater 130nm process technology. Its 
   comprehensive set of files, libraries, and guidelines streamline the design process and facilitate the creation of high-quality integrated circuits.

   > *You can refer to skywater130 manual [here](https://skywater-pdk.readthedocs.io/en/main/)*

 **Yosys -- Yosys Open SYnthesis Suite**
![image](https://github.com/SudeepGopavaram/Physical_Design_Using_OpenLane_Flow/assets/57873021/61878d69-c9fe-4f25-86e1-989ac45dea4d)

This tool is used to perform any synthesis job it is a framework for verilog RTL synthesis and provides a basic set of synthesis algorithms for various application domains


# Chip Planning Terminology
Physical design process starts with the *Chip Planning*. Physical Design implementation is strongly depends on the size of design and for large system we decompose them into the sub-systems or blocks which is also known as *partitioning*.

After partitioning we determine the location of each block and macros. we carry out pin assignment, define the location of input and output pads, allocatin adequate space for creating rows of standard cells which is known as floorplaning

Power planning is also done during the chip planning phase.

* **DIE-SIZE** - For layout to be created we need to first define the die size and its aspect ratio. Ideally die size should be as small as possible which will allow us to fabricate more chips for a given wafer area, also reducing area reduces the cost of the chip also enables us to achieve a higher yield for smaller die.

Die-Size should be able to accomodate the following entities:

**1. Blocks** - A separate space need to be allocated on the layout for larger instances or blocks or macros. These blocks can obtained after partitioning or it can be functional blocks like processors, memories or analog blocks.

**2. Standard Cell** - Standard cell are placed on a die therefore a dedicated space is allocated for them. Area required for the standard cells can be estimated using the given netlist and the corresponding technology library.

**3. Pads** - I/O pads are required for the signals to enter or leave from a chip. Also power must be delivered to the chip using power and ground pads.

**4. Interconnects** - There must be provision of interconnects in the layout but during floorplan stage, the layout of the interconnect is not yet decided so it is challenging to estimate the area we must allocate for the interconnects on the die.

**5. Core Utilization or Core Area** - It is the die area excluding the area of the I/O pads and the power pads this is know as *core utilization*.

**6. Package** - It is a protective case that surrounds the circuit material to protect it from physical damage or corrosion and allow mounting of electrical contacts connecting it ti the PCB. Below shown snippet shows IC with 48 pins and Quad Flat No-Leads(QFN) package.


![image](https://github.com/SudeepGopavaram/Physical_Design_Using_OpenLane_Flow/assets/57873021/95842423-0621-478f-b4e4-85212be5c3e3)
