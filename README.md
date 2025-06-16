# Digital-VLSI-SoC-design-and-planning

## Contents
## 📘 Session 1 - Inception of Open-Source EDA, OpenLANE and Sky130 PDK 

### 🔬 Theory
This section introduces the basics of open-source EDA tools, OpenLANE flow, and Sky130 PDK. It explains how open-source efforts enable VLSI enthusiasts and students to carry out industry-grade digital SoC implementation flows.

#### Tasks:
- ✅ Run `picorv32a` design synthesis using OpenLANE flow and generate necessary outputs  
- ✅ Calculate the Flop Ratio

### ⚙️ Implementation

1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.

![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day1/flow%20.png)

![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day1/synthesis.png)

2. Calculate the flop ratio.
Screenshots of synthesis statistics report file with required values highlighted

![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day1/flop%20ratio.png)

## Synthesis Statistics
- **Total number of cells** = 14876  
- **Number of flip-flops (sky130_fd_sc_hd__dfxtp_2)** = 1613

**Flop Ratio**  
Flop Ratio = 1613 / 14876 = 0.108429685

**Percentage of DFFs**  
Percentage of DFFs = 0.108429685 × 100 = **10.84296854%**



## 📘 Session 2 - Good floorplan vs bad floorplan and introduction to library cells

### 🔬 Theory

#### Tasks:
   
- ✅ Run the picorv32a design floorplanning using the OpenLANE flow, and generate the necessary output files.
- ✅ Calculate the die area in microns using the values from the generated floorplan DEF file:
-              Die Area=Die Width (µm)×Die Height (µm)
- ✅ Load the generated floorplan DEF file in the Magic layout tool and explore the floorplan.
- ✅ Run congestion-aware placement for the picorv32a design using the OpenLANE flow, and generate the necessary output files.
- ✅ Load the generated placement DEF file in Magic and explore the placement.

### ⚙️ Implementation

1. Run `picorv32a` design floorplan using OpenLANE flow and generate necessary outputs.  
   Commands to invoke the OpenLANE flow and perform floorplan are as follows:
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/floorplan.png)
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/floorplanc.png)

2. Calculate the die area in microns from the values in the floorplan DEF file.  
   Below is a screenshot or snippet showing the relevant part of the `floorplan.def` file:

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/dia%20area%20.png)
   Die Area Calculation from `floorplan.def`
   Unit Distance:
   1000 units = 1 micron

   Die Dimensions (in Unit Distance):
 - Die Width  = 660685 − 0 = **660685 units**
 - Die Height = 671405 − 0 = **671405 units**

   Convert to Microns:
   Die Width (µm)  = 660685 / 1000 = **660.685 µm**
   Die Height (µm) =  671405 / 1000 = **671.405 µm**

   Die Area (in Square Microns):
   Die Area = Width × Height = 660.685 × 671.405  
                            = **443,587.212425 µm²**
      
3. Load generated floorplan def in magic tool and explore the floorplan.

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/magic1.png)

 - Equidistant placement of ports
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/equdistance.png)
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/equidistance2.png)

 - Port layer as set through config.tcl
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/1metal.png)
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/2metal.png)

 - Unplaced standard cells at the origin
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/standard%20cell.png)

4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/runplacement.png)

5. Load generated placement def in magic tool and explore the placement.
  ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/placementcomand.png)

 - Screenshots of floorplan def in magic
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/placementlayout.png)

 - Standard cells legally placed
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/standard%20cell%20placed.png)



## 📘 Session 3 - Design library cell using Magic Layout and ngspice characterization 

### 🔬 Theory

#### Tasks:
- ✅ Clone the GitHub repository that contains the custom inverter standard cell design created using the OpenLANE flow.
- ✅ Open the custom inverter layout using the Magic VLSI tool and examine its structure and design.
- ✅ Perform SPICE netlist extraction of the inverter from within Magic.
- ✅ Modify the extracted SPICE model file to prepare it for circuit simulation and analysis.
- ✅ Run post-layout simulations using ngspice to verify the functionality of the inverter.
- ✅ Identify and resolve issues in the DRC (Design Rule Check) section of the older Magic technology file for the SkyWater process.

### ⚙️ Implementation :
1. Clone the GitHub repository that contains the custom inverter standard cell design created using the OpenLANE flow.
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/copy%20command.png)

2. Open the custom inverter layout using the Magic VLSI tool and examine its structure and design.
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/inerter%20layout.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/nmos.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/pmos.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/gnd.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/pwr.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/drc%20error.png)
   
3. Perform SPICE netlist extraction of the inverter from within Magic.
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/extract%20spice%20.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/spiceext%20.png)
   
4. Modify the extracted SPICE model file to prepare it for circuit simulation and analysis.
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/spice%20commond.png)

5. Run post-layout simulations using ngspice to verify the functionality of the inverter.
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/ngspice%20commond.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/plot%20commond.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/plot.png)

i)Rise transition time calculation
  - 20% Screenshots
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/20%25.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/20%25%20comond.png)

  - 80% Screenshots
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/80%25.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/80%25commond.png)

ii) Fall transition time calculation
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/cell%20fall20%25.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/cell%20fall80%25.png)

iii) Rise Cell Delay Calculation
     ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/50%25.png)

     ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/bolb/main/Day3/50%25commond.png)

iv)  Fall Cell Delay Calculation
      ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/50%25fall.png)
   
6. Identify and resolve issues in the DRC (Design Rule Check) section of the older Magic technology file for the SkyWater process.
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/drc%20test%20comond.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/magiccrc1.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/magic%20crc2.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/poly.9.png)

   New commands inserted in sky130A.tech file to update drc
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/edit%20in%20sky1301.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/editin%20sky1302.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day3/drc%20checkin%20poly.png)










## 📘 Session 4 - Pre-layout timing analysis and importance of good clock tree 

### 🔬 Theory

#### Tasks:

### ⚙️ Implementation


## 📘 Session 5 - Final steps for RTL2GDS using tritonRoute and openSTA 
### 🔬 Theory

#### Tasks:

### ⚙️ Implementation













