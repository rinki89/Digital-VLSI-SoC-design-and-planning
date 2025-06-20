# Digital-VLSI-SoC-design-and-planning

## 📚 Table of Contents
- [Session 1: Inception of Open-Source EDA, OpenLANE and Sky130 PDK](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/README.md#-session-1---inception-of-open-source-eda-openlane-and-sky130-pdk)
- [Session 2: Good floorplan vs bad floorplan and introduction to library cells](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/README.md#-session-2---good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells)
- [Session 3: Design library cell using Magic Layout and ngspice characterization](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/README.md#-session-3---design-library-cell-using-magic-layout-and-ngspice-characterization)
- [Session 4: Pre-layout timing analysis and importance of good clock tree](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/README.md#-session-4---pre-layout-timing-analysis-and-importance-of-good-clock-tree)
- [Session 5: Final steps for RTL2GDS using tritonRoute and openSTA](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/README.md#-session-5---final-steps-for-rtl2gds-using-tritonroute-and-opensta)
- [Acknowledgements](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/README.md#%EF%B8%8F-acknowledgements)

#
## 📘 Session 1 - Inception of Open-Source EDA, OpenLANE and Sky130 PDK 

### 🔬 Theory
This section introduces the basics of open-source EDA tools, OpenLANE flow, and Sky130 PDK. It explains how open-source efforts enable VLSI enthusiasts and students to carry out industry-grade digital SoC implementation flows.

#### Tasks:
- ✅ Run _picorv32a_ design synthesis using OpenLANE flow and generate necessary outputs  
- ✅ Calculate the Flop Ratio

### ⚙️ Implementation

1. Run _picorv32a_ design synthesis using OpenLANE flow and generate necessary outputs.<br>
   Commands to invoke the OpenLANE flow and perform floorplan are as follows:<br>
-  Change directory to openlane flow directory to begin using the OpenLANE flow, first navigate to the OpenLANE working directory by running:
   `cd ~/Desktop/work/tools/openlane_working_dir/openlane`<br>
-  Once the alias is set up, simply run `docker` to start the OpenLANE Docker container.<br>
-  you can launch OpenLANE in interactive mode by running `./flow.tcl -interactive` then load the required tcl package `package require openlane 0.9`. <br>
-  Prepare the design environment for picorv32a `prep -design picorv32a`.
  
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day1/flow%20.png)

    Once the design is prepped, you can begin first running synthesis `run_synthesis`.
    
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day1/synthesis.png)

2. Calculate the flop ratio.<br>
   Screenshots of synthesis statistics report file with required values.
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day1/flop%20ratio.png)

   __Synthesis Statistics__ :
   <p>Total number of cells = 14876</p>
   <p>Number of flip-flops (sky130_fd_sc_hd__dfxtp_2) = 1613</p>
   <p>Flop Ratio = 1613 / 14876 = 0.108429685</p>
   <p>Percentage of DFFs = 0.108429685 × 100 = <strong>10.84296854%</strong></p>


##
## 📘 Session 2 - Good floorplan vs bad floorplan and introduction to library cells

### 🔬 Theory

#### Tasks:
   
- ✅ Run the _picorv32a_ design floorplanning using the OpenLANE flow, and generate the necessary output files.
- ✅ Calculate the die area in microns using the values from the generated floorplan DEF file:<br>
               Die Area=Die Width (µm)×Die Height (µm)
- ✅ Load the generated floorplan DEF file in the Magic layout tool and explore the floorplan.
- ✅ Run congestion-aware placement for the picorv32a design using the OpenLANE flow, and generate the necessary output files.
- ✅ Load the generated placement DEF file in Magic and explore the placement.

### ⚙️ Implementation

1. Run _picorv32a_ design floorplan using OpenLANE flow and generate necessary outputs.<br>
   After synthesis completes, proceed to floorplanning with commond `run_floorplan`

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day2/floorplan.png)
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day2/floorplanc.png)

2. Calculate the die area in microns from the values in the floorplan DEF file.  
   Below is a screenshot or snippet showing the relevant part of the _floorplan.def_ file:
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day2/dia%20area%20.png)
   
   __Die Area Calculation from _floorplan.def___
   <p>Unit Distance: 1000 units = 1 micron</p>
   <p>Die Dimensions (in Unit Distance):<br>
    Die Width = 660685 − 0 = 660685 units<br>
    Die Height = 671405 − 0 = 671405 units</p>
    <p>Convert to Microns:<br>
     Die Width (µm) = 660685 / 1000 = 660.685 µm<br>
     Die Height (µm) = 671405 / 1000 = 671.405 µm</p>
    <p>Die Area (in Square Microns):<br>
     Die Area = Width × Height = 660.685 × 671.405<br>
                               = 443,587.212425 µm²</p>
      
3. Load generated floorplan def in magic tool and explore the floorplan.<br>
   To see the actual layout after the flow, we have to open the magic file by adding the command <br>`magic-T/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def`

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day2/magic1.png)

 - Equidistant placement of ports.<br>
   To select an object, click on it and then press 's' on your keyboard the object will be highlighted. <br>
   To zoom in, click the object and press 'z' and To zoom out, use Shift + z.
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day2/equdistance.png)
   
   In the above layout we can see that, input output pins are at equal distance.
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day2/equidistance2.png)

 - Port layer as set through config.tcl
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day2/1metal.png)

   Launch the tkcon window and enter the command `what` to get detailed information about a specific pin. <br>
   For instance, it shows that a particular pin is placed on Metal 3. Likewise, inspecting the vertical pins reveals they are located on Metal 2.

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day2/2metal.png)

 - Unplaced standard cells at the origin
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day2/standard%20cell.png)

4. Run _picorv32a_ design congestion aware placement using OpenLANE flow and generate necessary outputs.
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day2/runplacement.png)

5. Load generated placement def in magic tool and explore the placement.

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day2/placementcomand.png)

 - Screenshots of _floorplan def_ in magic
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day2/placementlayout.png)

 - Standard cells legally placed
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day2/standard%20cell%20placed.png)


##
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
1. Clone the GitHub repository that contains the custom inverter standard cell design created using the OpenLANE flow.<br>
   To clone the repository, run the command in the OpenLane terminal <br> `git clone https://github.com/nickson-jose/vsdstdcelldesign`<br> This will create a folder named vsdstdcelldesign inside the OpenLane directory.
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/copy%20command.png)
   
   After cloning, copy the Magic tech file by running <br>`cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .`<br>
   Once these steps are completed, you will find the vsdstdcelldesign folder inside the OpenLane directory, along with the required sky130A.tech file.

2. Open the custom inverter layout using the Magic VLSI tool and examine its structure and design.<br>
   Command to open custom inverter layout in magic <br> `magic -T sky130A.tech sky130_inv.mag & .` 
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/inerter%20layout.png)

   Identification of NMOS and PMOS
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/nmos.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/pmos.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/gnd.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/pwr.png)
   
   The PMOS source connection to VDD (labeled as VPWR) has been verified, and the NMOS source connection to VSS (labeled as VGND) has also been confirmed.

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/drc%20error.png)
   
4. Perform SPICE netlist extraction of the inverter from within Magic.<br>
     To perform SPICE extraction for the custom inverter layout in the Magic tkcon window, first run the command `extract all` to generate the '.ext' file from the layout.<br>
     Next, use `ext2spice cthresh 0 rthresh 0` to enable parasitic extraction by setting both the capacitance and resistance thresholds to zero.<br>
     Finally, run `ext2spice` to convert the extracted data into a SPICE netlist.
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/extract%20spice%20.png)

   let's see what inside the spice file by commond `vim sky130_inv.spice`.
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/spiceext%20.png)
   
5. Modify the extracted SPICE model file to prepare it for circuit simulation and analysis.
   
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/spice%20commond.png)
   
   To set up the SPICE simulation, include the model files with _.include ./libs/pshort.lib_ and _.include ./libs/nshort.lib_.<br>
   Set VDD using VDD VPWR 0 3.3V and VSS accordingly.<br>
   Define the input with Va A VGND PULSE(0V 3.3V 0 0.1ns 2ns 4ns). <br>
   Add the analysis commands: .tran 1n 20n, .control, run, .endc, and .end.

6. Run post-layout simulations using ngspice to verify the functionality of the inverter.
   
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/ngspice%20commond.png)

    Now, ploting the graph here by command, `plot y vs time a`.
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/plot%20commond.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/plot.png)

  i)__Rise transition time calculation__
  - 20% Screenshots
      ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/20%25.png)

  - 80% Screenshots
      ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/80%25.png)

      ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/80%25comnd.png)
   
       <p>20% of output = 660 mV</p>
       <p>80% of output = 2.64 V</p>
       <p>Rise transition time = Time taken for output to rise to 80% − Time taken for output to rise to 20%</p>
                                                =2.24706 - 2.17976 = 0.0673 ns = 67.3 ps</p>         

    ii) __Fall Transition Time Calculation__
    
     ![image](https://raw.githubusercontent.com/rinki89/Digital-VLSI-SoC-design-and-planning/main/Pictures/Day3/cell%20fall20%25.png)
    
     ![image](https://raw.githubusercontent.com/rinki89/Digital-VLSI-SoC-design-and-planning/main/Pictures/Day3/cell%20fall80%25.png)
    
       <p>20% of output = 660 mV</p>
       <p>80% of output = 2.64 V</p>
       <p>Fall transition time = Time taken for output to fall to 20% − Time taken for output to fall to 80%</p>
                                             <p>= 4.09375 − 4.05127 = 0.04248 ns = 42.48 ps</p>
    
    iii) __Rise Cell Delay Calculation__
    
     ![image](https://raw.githubusercontent.com/rinki89/Digital-VLSI-SoC-design-and-planning/main/Pictures/Day3/50%25.png)
    
     ![image](https://raw.githubusercontent.com/rinki89/Digital-VLSI-SoC-design-and-planning/main/Pictures/Day3/50%25commond.png)

     <p>50% of 3.3 V = 1.65 V</p>
     <p>Rise Cell Delay = Time taken for output to rise to 50% − Time taken for input to fall to 50%</p>
                                     <p> = 2.21208 − 2.1497 = 0.06238 ns = 62.38 ps</p>
   

    iv) __Fall Cell Delay Calculation__
    
     ![image](https://raw.githubusercontent.com/rinki89/Digital-VLSI-SoC-design-and-planning/main/Pictures/Day3/50%25fall.png)
   
      <p>50% of 3.3 V = 1.65 V</p>
       <p>Fall Cell Delay = Time taken for output to fall to 50% − Time taken for input to rise to 50%</p>
                                        <p>= 4.0763 − 4.05011 = 0.02619 ns = 26.19 ps</p>


   
6. Identify and resolve issues in the DRC (Design Rule Check) section of the older Magic technology file for the SkyWater process.<br>
   Link to Sky130 Periphery rules: https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html <br>
   To extract the lab files, use `tar xfz drc_tests.tgz`, then navigate into the drc_tests folder. List all contents with `ls -al`.
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/drc%20test%20comond.png)

   To view the .magicrc file, use `gvim .magicrc` this file configures Magic and points to the local tech file.<br>
   To launch Magic with enhanced graphics, run `magic -d XR &.` .
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/magiccrc1.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/magic%20crc2.png)

   To launch Magic with enhanced graphics, run `magic -d XR &.` .
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/poly.9.png)
   Incorrectly implemented poly.9 rule no drc violation even though spacing < 0.48u

   New commands inserted in _sky130A.tech_ file to update drc
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/edit%20in%20sky1301.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/editin%20sky1302.png)

   In the tkcon window, load the updated tech file with `tech load sky130A.tech` <br>
   then run `drc check` to recheck for errors, and use `drc why` to view details of the violations.
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/drc%20checkin%20poly.png)

   Incorrectly implemented difftap.2 simple rule correction
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/incorect%20diff2.png)
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/1st%20challenge.png)
   
   Now we will make some changes in _sky130A.tech_ file which are as follows:
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/edit%20for%202nd%20chlng.png)
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/edit%20for%202ndchlg%201.png)

   Commands to run in tkcon window<br>
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/error%20in%20nwell.png)

   Incorrectly implemented nwell.4 rule no drc violation even though no tap present in nwell

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day3/last.png)

##
## 📘 Session 4 - Pre-layout timing analysis and importance of good clock tree 

### 🔬 Theory

#### Tasks:
- ✅ Fix up small DRC errors and verify the design is ready to be inserted into our flow.
- ✅ Save the finalized layout with custom name and open it.  
- ✅ Generate lef from the layout.  
- ✅ Copy the newly generated lef and associated required lib files to _picorv32a_ design _src_ directory.  
- ✅ Edit _config.tcl_ to change lib file and add the new extra lef into the openlane flow.  
- ✅ Run openlane flow synthesis with newly inserted custom inverter cell.  
- ✅ Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.  
- ✅ Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.  
- ✅ Do Post-Synthesis timing analysis with OpenSTA tool.  
- ✅ Make timing ECO fixes to remove all violations.  
- ✅ Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.  
- ✅ Post-CTS OpenROAD timing analysis.  
- ✅ Explore post-CTS OpenROAD timing analysis by removing _sky130_fd_sc_hd__clkbuf_1_ cell from clock buffer list variable _CTS_CLK_BUFFER_LIST_.

  ### ⚙️ Implementation
  
1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.
  - Conditions to Verify Before Proceeding with the Custom Standard Cell Layout:<br>
     i) The input and output ports must be aligned at the intersection points of horizontal and vertical routing tracks.<br>
    ii) The cell width must be an odd multiple of the horizontal track pitch.<br>
    iii) The cell height must be an even multiple of the vertical track pitch.<br>
    
    Change to the sky130 Directory by using commond <br>
    `cd ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd` .
    
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/tracks%20commond.png)
    
    open the tracks.info file by commond `less tracks.info`.
    
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/less%20tracks.png)
    
    Commands for tkcon window to set grid as tracks of locali layer

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/grid%20commond.png)
    
    Get Syntax for the grid Command by `help grid` <br>
    Set Grid Values `grid 0.46um 0.34um 0.23um 0.17um` <br>
    The values typically mean:0.46um – X grid spacing, 0.34um – Y grid spacing, 0.23um – Snap resolution, 0.17um – Search distance.

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/after%20gridcomomd.png)
    
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/grid.png)

  - Condition 1 verified
    
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/condition1.png)

  - Condition 2 verified
    
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/width.png)
    
    Horizontal Track Pitch = 0.46 µm<br>
    Width of Standard Cell = 1.38 µm = 0.46 µm × 3 (i.e., 3 × horizontal track pitch)

  - Condition 3 verified
    
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/length.png)
    
    Vertical Track Pitch = 0.34 µm<br>
    Height of Standard Cell = 2.7 µm = 0.34 µm × 8 (i.e., 8 × vertical track pitch)
 
2. Save the finalized layout with custom name and open it.
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/commond1.png)
   
3. Generate lef from the layout.
   in tkcon window run the command to extract the LEF file `lef write` .
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/leffile.png)
   
   Screenshot of newly created lef file
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/lef%20file.png)
   
4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
   Screenshot of commands run<br>`cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/`
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/cmdcopyof%20invfile.png)

   List and check whether it's copied<br>`ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/`

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/copyinsrc.png)

5. Edit _config.tcl_ to change lib file and add the new extra lef into the openlane flow.
  
   `set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib<br>
   set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib<br>
   set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib<br>
   set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib`<br>

   set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/configedit.png)
   
6. Run openlane flow synthesis with newly inserted custom inverter cell.
  
   Change directory to openlane flow directory to begin using the OpenLANE flow, first navigate to the OpenLANE working directory by running:
   `cd ~/Desktop/work/tools/openlane_working_dir/openlane`<br>
-  Once the alias is set up, simply run `docker` to start the OpenLANE Docker container.<br>
-  you can launch OpenLANE in interactive mode by running `./flow.tcl -interactive` then load the required tcl package `package require openlane 0.9`. <br>
-  Prepare the design environment for picorv32a `prep -design picorv32a`.<br>
-  Adiitional commands to include newly added lef to openlane flow<br>
   `set lefs [glob $::env(DESIGN_DIR)/src/*.lef]`<br>
   `add_lefs -src $lefs`<br>

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/docker.png)
   
- Now that the design is prepped run synthesis using command `run_synthesis`
  
  ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/runsynthesis.png)

  ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/synthesis%20done.png)

7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
   
   Noting down current design values generated before modifying parameters to improve timing
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/chiparea.png)

   Screenshot of merged.lef in tmp directory with our custom inverter as macro
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/mergedfile.png)

   Commands to view and change parameters to improve timing and run synthesis
-  Once again we have to prep design so as to update variables `prep -design picorv32a -tag 16-06_11-34 -overwrite`.<br>

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/1.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/slack0.png)

   Comparing to previously noted run values area has increased and worst negative slack has become 0.
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/areardus.png)
   

8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
   Alternative to run_floorplan Command in OpenLANE If you're encountering unexpected or unexplained errors while using the standard `run_floorplan` command.
   Use the Following Commands Instead of `run_floorplan`:
   `init_floorplan`
   `place_io`
   `tap_decap_or`
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/runflrplan.png)

   Now we are ready to run placement `run_placement`
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/plcment.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/plcmentdone.png)

   Commands to load placement def in magic tool in another terminal <br>
   `magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &`
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/layout1.png)

   Screenshot of custom inverter inserted in placement def with proper abutment
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/vsdinv.png)

   Command for tkcon window to view internal layers of cells `expand`
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/expand.png)

9. Do Post-Synthesis timing analysis with OpenSTA tool.
    
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/synthesis%20done.png)

   Newly created _pre_sta.conf_ for STA analysis in openlane directory
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/presta.png)

   Newly created _my_base.sdc_ for STA analysis in _openlane/designs/picorv32a/src_ directory based on the file _openlane/scripts/base.sdc_
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/copy%20base.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/editmybase.png)

   Command to invoke OpenSTA tool with script `sta pre_sta.conf`

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/pre_sta1.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/sta2.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/sta3.png)
   
   Since more fanout is causing more delay we can add parameter to reduce fanout and do synthesis again<br>
   Commands to include new lef and perform synthesis
-  Use the _prep_ command to initialize the environment for the _picorv32a design_. The _-tag_ creates a uniquely named run directory, and _-overwrite_ clears any previous run with the same tag.<br>
   `prep -design picorv32a -tag 16-06_16-22 -overwrite`<br>
-  Add Custom LEF Files<br>
   `set lefs [glob $::env(DESIGN_DIR)/src/*.lef]`<br>
   `add_lefs -src $lefs`<br>
-  Enable synthesis sizing set<br> ::env(SYNTH_SIZING) 1`<br>
-  Set maximum fanout <br>`set ::env(SYNTH_MAX_FANOUT) 4`<br>
-  Check the current driving cell <br>`echo $::env(SYNTH_DRIVING_CELL)`<br>
-  With the design prepped and parameters updated, initiate the synthesis step <br>`run_synthesis`

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/synth2.png)

   Commands to run STA in another terminal again by 
   `sta pre_sta.conf`
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/presta21.png)
   
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/presta22.png)
   
10. Make timing ECO fixes to remove all violations.
    OR gate of drive strength 2 is driving 4 fanouts
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/or%20gate.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/cmnd.png)

    Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/violation1.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/or2.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/cmnd2.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/or3.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/cmnd3.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/or4.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/cmnd4.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/violation2.png)

    Commands to verify instance _14506_ is replaced with sky130_fd_sc_hd__or4_4
    Screenshot of replaced instance
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/or5.png)

    
11. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
    Commands to write verilog
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/verilogcmnd.png)

    Verified that the netlist is overwritten by checking that instance _14506_ is replaced with sky130_fd_sc_hd__or4_4
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/_14506.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/ctscmnd.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/ctsdone.png)

12. Post-CTS OpenROAD timing analysis.
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/openroad.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/check1.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/2.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/3.png)

13. Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.
    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/4.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/5.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/6.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/7.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/8.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/9.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/10.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/11.png)

    ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day4/12.png)
    
##
## 📘 Session 5 - Final steps for RTL2GDS using tritonRoute and openSTA 
### 🔬 Theory

#### Tasks:

- ✅ Perform generation of Power Distribution Network (PDN) and explore the PDN layout.
- ✅ Perfrom detailed routing using TritonRoute.
- ✅ Post-Route parasitic extraction using SPEF extractor.
- ✅ Post-Route OpenSTA timing analysis with the extracted parasitics of the route.
  
### ⚙️ Implementation

1. Perform generation of Power Distribution Network (PDN) and explore the PDN layout.
   Commands to perform all necessary stages up until now
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/1.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/2.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/3.png)

   Screenshots of PDN def
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/6.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/7.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/8.png)

2. Perfrom detailed routing using TritonRoute and explore the routed layout.
   Command to perform routing
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/9.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/10.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/11.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/12.png)

   Commands to load routed def in magic in another terminal
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/13.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/14.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/15.png)

   Screenshot of fast route guide present in openlane/designs/picorv32a/runs/16-06_16-56/tmp/routing directory
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/16.png)

3. Post-Route parasitic extraction using SPEF extractor.
   Commands for SPEF extraction using external tool
   The next step involves post-routing STA analysis, which requires the extraction of parasitic effects (SPEF).Since OpenLANE does not have a SPEF extraction tool, this process needs to     be done outside of OpenLANE.
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/Screenshot%20from%202025-06-17%2016-02-24.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/Screenshot%20from%202025-06-17%2016-02-59.png)

   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/Screenshot%20from%202025-06-17%2016-06-43.png)
   
   This is the final generated layout.
   ![image](https://github.com/rinki89/Digital-VLSI-SoC-design-and-planning/blob/main/Pictures/Day5/Screenshot%20from%202025-06-17%2016-06-53.png)

   ### ✍️ Acknowledgements
   **Kunal Ghosh**<br>
   Co-founder, VSD Corp. Pvt. Ltd.

   **Nickson P Jose**<br>
   Physical Design Engineer, Intel Corporation

   **R. Timothy Edwards**<br>
   Senior Vice President of Analog and Design, efabless Corporation
    













