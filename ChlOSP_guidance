This documents outlines the steps needed to run an ocean hindcast CESM simulation with ChlOSP, the Chlorophyll Observation Simulator Package. 

**Step 1: Download code** </br>
Run the following commands: 
  1. `git clone -b isccp_datm https://github.com/genna-clow/CESM.git cesm_chlosp` </br>
  2. `cd cesm_chlosp` </br>
  3. `./manage_externals/checkout_externals` </br>

  The `checkout_externals` command pulls code from the component repositories, which are listed in **Externals.cfg**.

**Step 2: Create new case** </br>
  1. `cd cime/scripts`
  2. `./create_newcase --case CASEDIR/g.e22.GOMIPECOIAF_JRA.TL319_g17_sst --res TL319_g17 --compset GOMIPECOIAF_JRA-1p4-2018 --run-unsupported` where CASEDIR is the path to the directory where you want to store your case. </br> 
More information on [component sets](https://docs.cesm.ucar.edu/models/cesm2/config/compsets.html) and [grids](https://docs.cesm.ucar.edu/models/cesm2/config/grids.html)

**Step 3: Build and submit case** 
  1. `cd CASEDIR/g.e22.GOMIPECOIAF_JRA.TL319_g17_sst`
  2. `./case.setup`
  3. Create new file: Buildconf/datmconf/datm.streams.txt.CORE_IAF_JRA.ISCCP.CLOUDS 
  4. Copy datm.streams.txt.CORE_IAF_JRA.ISCCP.CLOUDS to case directory and append ‘user_’ 
  5. Copy datm_ from BuildConf and append ‘user_’ 
  6. Modify user_nl_datm 
  7. `./xmlchange RUN_STARTDATE=1897-01-01`
  8. Follow instructions here for adding new MARBL diagnostic: https://readthedocs.org/projects/marbl/downloads/pdf/latest/ 
  9. Copied ecosys_diagnostics to SourceMods/src.pop/ecosys_diagnostics and edited frequency of outputs (sat_average) 
  10. Added daily surface nutrient limitations, light limitations, and chlorophyll for each phytoplankton type 
  11. `qcmd -A P93300670 -- ./case.build`
  12. `./xmlchange JOB_WALLCLOCK_TIME=12:00:00`
  13. `./xmlchange JOB_WALLCLOCK_TIME=01:00:00 --subgroup case.st_archive` 
  14. `./xmlchange STOP_OPTION=nyears`
  15. `./xmlchange STOP_N=3` 
  16. `./xmlchange RESUBMIT=39` 
  17. `./case.submit`

Please see [this page](https://escomp.github.io/CESM/versions/cesm2.2/html/introduction.html) for more information on downloading, building and running CESM2. 
