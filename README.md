# Physical_Design_using_OpenLANE_Sky130-PDK

# Introduction:
OpenLane is an RTL to GDSII infrastructure library based on several components including OpenROAD, Yosys, Magic, Netgen, CVC, KLayout, and a number of custom scripts for design exploration and optimization. A reference flow performs all ASIC implementation steps from RTL all the way down to GDSII.

# Table of contents:
1. Stage 1:-Synthesis
2. Stage 2:-Floorplan
3. Stage 3:-Placement
4. Stage 4:-Clock Tree Synthesis(CTS)
5. Stage 5:-Power Distribution Network(PDN)
6. Stage 6:-Routing using Triton Route
7. Stage- 7 GDSII file
Additional:- Steps to build the standard cell  and its integration in the picorv32a

# Results only:
* All the Layout views are generated using Magic Tool.
  
# Stage 1:-Synthesis:-
The Command used:- run_synthesis
Results: Calculation of the flop ratio:1613/14876=0.1084%
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/e71f8beb-a1a2-46c2-b94b-fb66a7be34ab)

# Stage 2:-Floorplan
The Command used:- run _floorplan
Results:

![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/b7f2bdee-827f-4b5f-9576-405a1bf019c6)

![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/7ef45e7b-ac7f-4817-9423-2b79bb0fa680)
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/dbf5b7c4-557a-4344-a1a5-914a1f797dea)

# Stage 3:-Placement

The Command used:- run_placement
Results:
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/3a9d6d1e-1778-4a06-8eb7-5d739b6ad1f4)



# Stage 4:-Clock Tree Synthesis(CTS)
The Command used:- run_cts
Results: The Slack Generated is below:
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/070cf5c5-eebd-40ed-ab0a-0ecb0f146cbb)

# Stage 5:-Power Distribution Network(PDN)
The Command used:- gen_pdn
Results: To check  if the final pdn was successful we can check the pdn.def file.

# Stage 6:-Routing using Triton Route
The Command used:- run_routing
Results: The Final routing is done after approx time of 30min -1hr, we can check in the run results.

# Stage 7: GDSII File 
A GDS file is an integrated circuit design saved in GDSII Stream format. A GDS file is similar to a Gerber file; it comprises solder masks, geometry, layers, component labels, and the general layout of a circuit saved as a binary database.

In OpenLANE Flow the  GDSII file is generated in the results/signoff/magic directory.

Results: The Final output is shown below:-

![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/31e9dd1f-ad14-471a-a855-5bc6f16374dc)

# Additional- Steps to build the standard cell  and its integration in the picorv32a
* Creation of Standard cell inverter using the OpenLANE Flow and integrating it in the picorv32a*
  Steps to be followed:-
  1. First git clone the inverter cell repository into our run area.
  2. Then open the Layout using the Magic tool.
  3. Set the SPICE File and run the simulations.
  4. After the Simulations check the Rise and Fall time transitions.
  5. Set the ports and Grid Values of the inverter.
 To integrate the standard cell in OpenLane config.tcl file must be edited with the following commands:

set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130/sky130_fd_sc_hd__typical.lib"

set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130/sky130_fd_sc_hd__slow.lib"

set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130/sky130_fd_sc_hd__fast.lib"

set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) glob "$::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef"

After the integration, run the synthesis and check whether the cell has been dumped or not in our OpenLANE Flow.
Results: The integrated standard cell results are shown below:-


![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/7af6ba2d-b09b-4304-9f42-d0eda4f33820)


![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/c328aef2-de35-46cd-8a5e-e22fcef7b2f5)



# Acknowledgements
- Kunal Gosh
- Nickson Jose
  





















   
