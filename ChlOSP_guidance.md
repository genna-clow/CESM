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
  3. Create new file: `Buildconf/datmconf/datm.streams.txt.CORE_IAF_JRA.ISCCP.CLOUDS` (see example file below)
  4. Copy new file (datm.streams.txt.CORE_IAF_JRA.ISCCP.CLOUDS) to case directory and append ‘user_’ to file name
  5. Modify user_nl_datm (see example file below)
  6. `./xmlchange RUN_STARTDATE=1897-01-01`
  7. `qcmd -A P93300670 -- ./case.build`
  8. `./xmlchange JOB_WALLCLOCK_TIME=12:00:00`
  9. `./xmlchange JOB_WALLCLOCK_TIME=01:00:00 --subgroup case.st_archive` 
  10. `./xmlchange STOP_OPTION=nyears`
  11. `./xmlchange STOP_N=3` 
  12. `./xmlchange RESUBMIT=39` 
  13. `./case.submit`

Please see [this page](https://escomp.github.io/CESM/versions/cesm2.2/html/introduction.html) for more information on downloading, building and running CESM2. 


**File Modifications** 

datm.streams.txt.CORE_IAF_JRA.ISCCP.CLOUDS:
```
<?xml version="1.0"?>
<file id="stream" version="1.0">
<dataSource>
   GENERIC
</dataSource>
<domainInfo>
  <variableNames>
     time    time
        xc      lon
        yc      lat
        area    area
        mask    mask
  </variableNames>
  <filePath>
     /glade/p/cesmdata/cseg/inputdata/atm/datm7/JRA55
  </filePath>
  <fileNames>
     domain.atm.TL319.151007.nc
  </fileNames>
</domainInfo>
<fieldInfo>
   <variableNames>
     cldamt  cloudfrac
   </variableNames>
   <filePath>
     /glade/work/gclow/isccp_data_TL319/yearly_files
   </filePath>
   <fileNames>
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1958.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1959.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1960.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1961.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1962.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1963.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1964.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1965.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1966.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1967.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1968.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1969.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1970.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1971.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1972.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1973.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1974.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1975.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1976.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1977.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1978.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1979.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1980.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1981.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1982.nc
      ISCCP-Basic.HGG.GLOBAL.TL319.climatology.1983.nc
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1984.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1985.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1986.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1987.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1988.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1989.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1990.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1991.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1992.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1993.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1994.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1995.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1996.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1997.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1998.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.1999.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2000.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2001.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2002.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2003.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2004.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2005.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2006.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2007.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2008.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2009.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2010.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2011.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2012.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2013.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2014.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2015.GPC.10KM.CS00.EA1.00.nc 
      ISCCP-Basic.HGG.v01r00.GLOBAL.TL319.2016.GPC.10KM.CS00.EA1.00.nc
      ISCCP-Basic-icdr.HGG.v01r00.GLOBAL.TL319.2017.GPC.10KM.CS00.EA1.00.nc
      ISCCP-Basic-icdr.HGG.v01r00.GLOBAL.TL319.2018.GPC.10KM.CS00.EA1.00.nc
   </fileNames>
   <offset>
      0
   </offset>
</fieldInfo>
</file>
```


user_nl_pop:
```
datamode = "CORE_IAF_JRA"
domainfile = "/glade/p/cesmdata/cseg/inputdata/share/domains/domain.lnd.TL319_gx1v7.170705.nc"
dtlimit = 1.5, 1.5, 1.5, 1.5, 1.5, 1.5, 1.5, 1.5, 1.5, 1.5, 1.0e30
fillalgo = "nn", "nn", "nn", "nn", "nn", "nn", "nn", "nn", "nn", "nn", "copy"
fillmask = "nomask", "nomask", "nomask", "nomask", "nomask", "nomask",
    "nomask", "nomask", "nomask", "nomask", "nomask"
fillread = "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET",
    "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET"
fillwrite = "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET",
    "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET"
mapalgo = "bilinear", "bilinear", "bilinear", "bilinear", "bilinear",
    "bilinear", "bilinear", "bilinear", "bilinear", "nn", "bilinear"
mapmask = "nomask", "nomask", "nomask", "nomask", "nomask", "nomask",
    "nomask", "nomask", "nomask", "nomask", "nomask"
mapread = "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET",
    "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET"
mapwrite = "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET",
    "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET", "NOT_SET"
readmode = "single", "single", "single", "single", "single", "single",
    "single", "single", "single", "single", "single"
streams = "datm.streams.txt.CORE_IAF_JRA_1p4_2018.GCGCS.PREC 1958 1958 2018",
    "datm.streams.txt.CORE_IAF_JRA_1p4_2018.GISS.LWDN 1958 1958 2018",
    "datm.streams.txt.CORE_IAF_JRA_1p4_2018.GISS.SWDN 1958 1958 2018",
    "datm.streams.txt.CORE_IAF_JRA_1p4_2018.NCEP.Q_10 1958 1958 2018",
    "datm.streams.txt.CORE_IAF_JRA_1p4_2018.NCEP.SLP_ 1958 1958 2018",
    "datm.streams.txt.CORE_IAF_JRA_1p4_2018.NCEP.T_10 1958 1958 2018",
    "datm.streams.txt.CORE_IAF_JRA_1p4_2018.NCEP.U_10 1958 1958 2018",
    "datm.streams.txt.CORE_IAF_JRA_1p4_2018.NCEP.V_10 1958 1958 2018",
    "datm.streams.txt.presaero.clim_2000 1958 2000 2000",
    "datm.streams.txt.co2tseries.omip 1897 1897 2018",
    "datm.streams.txt.CORE_IAF_JRA.ISCCP.CLOUDS 1958 1958 2018"
taxmode = "cycle", "cycle", "cycle", "cycle", "cycle", "cycle", "cycle",
    "cycle", "cycle", "extend", "cycle"
tintalgo = "linear", "linear", "coszen", "linear", "linear", "linear",
    "linear", "linear", "linear", "linear", "linear"
vectors = "u:v"
```
