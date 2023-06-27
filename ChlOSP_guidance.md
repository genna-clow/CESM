This documents outlines the steps needed to run a fully-coupled, pre-industrial CESM simulation with ChlOSP, the Chlorophyll Observation Simulator Package. 

**Step 1: Download code** </br>
Run the following commands: 
  1. `git clone -b cesm2.2.0_satchl https://github.com/genna-clow/CESM.git cesm_chlosp` </br>
  2. `cd cesm_chlosp` </br>
  3. `./manage_externals/checkout_externals` </br> 

**Step 2: Create new case** </br>
  1. `cd cime/scripts`
  2. `./create_newcase --case CASEDIR/b.e22.B1850.f09_g17.cosp_chlor --res f09_g17 --compset B1850` where CASEDIR is the path to the directory where you want to store your case. </br> 
More information on [component sets](https://docs.cesm.ucar.edu/models/cesm2/config/compsets.html) and [grids](https://docs.cesm.ucar.edu/models/cesm2/config/grids.html)

**Step 3: Modify case** </br>
  1. `cd CASEDIR/b.e22.B1850.f09_g17.cosp_chlor_30yr`
  2. `./xmlchange JOB_WALLCLOCK_TIME=12:00:00` (increase job time)
  3. `./xmlchange JOB_WALLCLOCK_TIME=01:00:00 --subgroup case.st_archive`
  4. `./xmlchange --append CAM_CONFIG_OPTS='-cosp'` (enable COSP)
  5. `./xmlchange STOP_N=2, STOP_OPTION=nyears, RESUBMIT=24` (specify run length)
  6. `./case.setup`

**Step 4: Modify namelist file** </br>
In the file **user_nl_cam** within the case directory, add the following lines of text: </br>
```
docosp=.true. </br>
cosp_nradsteps=1 </br>
cosp_ncolumns=250 </br>
cosp_lmodis_sim = .true. </br>
cosp_lisccp_sim = .true. </br>
nhtfrq=0,-24 </br>
fincl2='CLTMODIS:A','CLDTOT_ISCCP:A','CLDTOT:A’ </br>
```
Decriptions of the namelist items can be found [here](https://docs.cesm.ucar.edu/models/cesm2/settings/current/cam_nml.html)

**Step 5: Build and submit case** 
  1. `./case.build` (or `qcmd -- ./case.build` if on Cheyenne)
  2. `./case.submit`

Please see [this page](https://escomp.github.io/CESM/versions/cesm2.2/html/introduction.html) for more information on downloading, building and running CESM2. 
