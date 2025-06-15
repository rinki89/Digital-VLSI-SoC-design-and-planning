# Digital-VLSI-SoC-design-and-planning

## Contents
## 📘 Session 1 - Inception of Open-Source EDA, OpenLANE and Sky130 PDK 

### 🔬 Theory
This section introduces the basics of open-source EDA tools, OpenLANE flow, and Sky130 PDK. It explains how open-source efforts enable VLSI enthusiasts and students to carry out industry-grade digital SoC implementation flows.

### ⚙️ Implementation

#### Tasks:

- ✅ Run `picorv32a` design synthesis using OpenLANE flow and generate necessary outputs  
- ✅ Calculate the Flop Ratio

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

### ⚙️ Implementation

#### Tasks:
   
- ✅ Run the picorv32a design floorplanning using the OpenLANE flow, and generate the necessary output files.
- ✅ Calculate the die area in microns using the values from the generated floorplan DEF file:
-              Die Area=Die Width (µm)×Die Height (µm)
- ✅ Load the generated floorplan DEF file in the Magic layout tool and explore the floorplan.
- ✅ Run congestion-aware placement for the picorv32a design using the OpenLANE flow, and generate the necessary output files.
- ✅ Load the generated placement DEF file in Magic and explore the placement.
  
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
Die Width (µm)  =  
660685 / 1000 = **660.685 µm**
Die Height (µm) =  671405 / 1000 = **671.405 µm**

Die Area (in Square Microns):
Die Area = Width × Height  
      = 660.685 × 671.405  
      = **443,587.212425 µm²**
      
3. Load generated floorplan def in magic tool and explore the floorplan.

![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/magic1.png)

Equidistant placement of ports
![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/equdistance.png)
![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/equidistance2.png)

Port layer as set through config.tcl
![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/1metal.png)
![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/2metal.png)

Unplaced standard cells at the origin
![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/standard%20cell.png)

4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/runplacement.png)

5. Load generated placement def in magic tool and explore the placement.
![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/placementcomand.png)

Screenshots of floorplan def in magic
![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/placementlayout.png)

Standard cells legally placed
![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Day2/standard%20cell%20placed.png)






## 📘 Session 3 - Design library cell using Magic Layout and ngspice characterization 
## 📘 Session 4 - Pre-layout timing analysis and importance of good clock tree 
## 📘 Session 5 - Final steps for RTL2GDS using tritonRoute and openSTA 













