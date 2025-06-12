# Digital-VLSI-SoC-design-and-planning

## Contents
## 📘 Day 1 - Inception of Open-Source EDA, OpenLANE and Sky130 PDK 

### 🔬 Theory
This section introduces the basics of open-source EDA tools, OpenLANE flow, and Sky130 PDK. It explains how open-source efforts enable VLSI enthusiasts and students to carry out industry-grade digital SoC implementation flows.

### ⚙️ Implementation

#### Tasks:

- ✅ Run `picorv32a` design synthesis using OpenLANE flow and generate necessary outputs  
- ✅ Calculate the Flop Ratio

1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.


## 📘 Day 2 - Good floorplan vs bad floorplan and introduction to library cells

### 🔬 Theory

### ⚙️ Implementation

#### Tasks:
   
- ✅ Run the picorv32a design floorplanning using the OpenLANE flow, and generate the necessary output files.
- ✅ Calculate the die area in microns using the values from the generated floorplan DEF file:
-              Die Area=Die Width (µm)×Die Height (µm)
- ✅ Load the generated floorplan DEF file in the Magic layout tool and explore the floorplan.
- ✅ Run congestion-aware placement for the picorv32a design using the OpenLANE flow, and generate the necessary output files.
- ✅ Load the generated placement DEF file in Magic and explore the placement.
1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
Commands to invoke the OpenLANE flow and perform floorplan

# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
  
## 📘 Day 3 - Design library cell using Magic Layout and ngspice characterization 
## 📘 Day 4 - Pre-layout timing analysis and importance of good clock tree 
## 📘 Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA 













