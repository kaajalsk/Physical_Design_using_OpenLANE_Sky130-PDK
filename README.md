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
   
*Additional:- Steps to build the standard cell  and its integration in the picorv32a.*

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

# The below steps are after including the standard cell.
# Stage 4:-Clock Tree Synthesis(CTS)
The Command used:- run_cts
Results: The generated new .def file is shown below:
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/a8d73a50-226a-430f-a495-f93a2eb51521)


# Stage 5:-Power Distribution Network(PDN)
The Command used:- gen_pdn
Results: To check  if the final pdn was successful we can check the pdn.def file.
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/b5d3994b-3534-42f6-b97c-9b134c7fd352)



# Stage 6:-Routing using Triton Route
The Command used:- run_routing
Results: The Final routing is done after approx time of 30min -1hr, we can check in the run results.
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/f2fd8941-2c5f-414e-915c-a93701f73d5d)


# Stage 7: GDSII File 
A GDS file is an integrated circuit design saved in GDSII Stream format. A GDS file is similar to a Gerber file; it comprises solder masks, geometry, layers, component labels, and the general layout of a circuit saved as a binary database.

In OpenLANE Flow the  GDSII file is generated in the results/signoff/magic directory.

Results: The Final output is shown below:-

![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/6c24a9f6-e9d1-4c86-9dc7-fc63a6b148ef)
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/a3bf3b48-7600-4dfc-85ec-8d8d09d40797)



# Additional- Steps to build the standard cell  and its integration in the picorv32a
* Creation of Standard cell inverter using the OpenLANE Flow and integrating it in the picorv32a.
* For more details we can go through https://github.com/nickson-jose/vsdstdcelldesign
  
  Steps to be followed:-
  1. First git clone the inverter cell repository into our run area.
  2. Then open the Layout using the Magic tool.
  3. Set the SPICE File and run the simulations.
  4. After the Simulations check the Rise and Fall time transitions.
  5. Set the ports and Grid Values of the inverter.
     
 * To integrate the standard cell in OpenLane config.tcl file must be edited with the following commands:-

set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130/sky130_fd_sc_hd__typical.lib"

set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130/sky130_fd_sc_hd__slow.lib"

set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130/sky130_fd_sc_hd__fast.lib"

set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) glob "$::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef"

* After the integration, run the synthesis and check whether the cell has been dumped or not in our OpenLANE Flow.

# Results: The integrated standard cell results are shown below:-
Inverter cell:
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/ab80f7a5-63b1-40e7-b54c-99c8388535f2)

SPICE extraction and Simulation:
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/0356f964-6ca3-44a2-9a3a-481c51cfe5a1)
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/a5b15cd1-a073-4866-a472-60bffe513002)
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/0233e91a-8d86-4b7f-9c8a-50da146cb105)

The included standard cell - sky130_vsdinv
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/4220b34c-3c62-4035-b8bc-a617e087138d)
![image](https://github.com/kaajalsk/Physical_Design_using_OpenLANE_Sky130-PDK/assets/141938909/ee51b00a-d55d-4d2d-bb9a-b8d4356645f5)















# Acknowledgements
- Kunal Gosh
- Nickson Jose
  





















   
