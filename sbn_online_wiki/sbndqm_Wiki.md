---
layout: page
title: SBN DQM Software Wiki
###subtitle: Specific Wiki for SBNDQM
description: Wiki documentation for SBNDQM
hero_height: is-small
toc: true
toc_title: SBNDQM Contents
---

The central hub for SBN Online Monitoring can be found here: [https://sbn-online.fnal.gov/](https://sbn-online.fnal.gov/)

sbndqm -- A Repository for SBN Online Monitoring
----------------------------------------------

The sbndqm code lives in this SBNSoftware repository: [https://github.com/SBNSoftware/sbndqm](https://github.com/SBNSoftware/sbndqm).

This repository is intended to house code for online monitoring in SBN and contains tooling for sending metrics to a database (through the artdaq MetricManager) and for receiving data from the artdaq Dispatcher (through the TransferInput module).

* [Instructions for using the metric manager](https://cdcvs.fnal.gov/redmine/projects/sbndqm/wiki/Metric_Management)
* [Instructions for using the TransferInput module](https://cdcvs.fnal.gov/redmine/projects/sbndqm/wiki/Receiving_Data_from_Artdaq)

All analysis code is located in sbndqm/sbndqm/dqmAnalysis. An example analysis using the Metric Manager resides in sbndqm/sbndqm/dqmAnalysis/example.

Minargon
----------------------------------------------
The online monitoring website that we use to view online DQM metrics for detector subsystems is called Minargon.
* For SBND, go here: [https://sbn-online.fnal.gov/cgi-bin/minargon/minargon.wsgi/introduction](https://sbn-online.fnal.gov/cgi-bin/minargon/minargon.wsgi/introduction)
* For ICARUS, go here: [https://sbn-online.fnal.gov/cgi-bin/icarus-minargon/icarus-minargon.wsgi/introduction](https://sbn-online.fnal.gov/cgi-bin/icarus-minargon/icarus-minargon.wsgi/introduction)


Workshop links
----------------------------------------------
* (First workshop instructions on redmine wiki)[https://cdcvs.fnal.gov/redmine/projects/sbndqm/wiki/Sbndqm_Workshop]


Developing in sbndqm
----------------------------------------------
sbndqm depends on _offline_ software, namely `sbncode`, and should be able to be developed in both online and offline computing environments.

Some guides for SBND Online monitoring development:
* [DQM Expert Guide](DQMExpertGuide.md)
* [Edit Minargon Website](EditMinargonWebsite.md)
* [Push Minargon Website](PushMinargonWebsite.md)

### Development in Offline Machine
To setup a development environment in an an offline machine (like `icarusgpvm, sbndgpvm`):
```
source /cvmfs/fermilab.opensciencegrid.org/products/artdaq/setup
source /cvmfs/icarus.opensciencegrid.org/products/icarus/setup_icarus.sh #(or /cvmfs/sbnd.opensciencegrid.org/products/sbnd/setup_sbnd.sh)

setup mrb
export MRB_PROJECT=sbndqm

mkdir <your_new_dev_area>
cd <your_new_dev_area>
mrb newDev -v v1_02_00 -q e20:prof #replace with your desired sbndqm version here!
source localProducts_sbndqm_*/setup 

cd srcs/
mrb g sbndqm
cd $MRB_BUILDDIR
mrbsetenv
mrb i -j8
```

Note: sometimes you may need to checkout a particular branch of the various code-base in order to get updates and proper dependencies. When that is the case, replace the `mrb g` commands with something like:
```
mrb g sbndqm@feature/update_Aug2023
mrb g sbndaq_online@feature/update_Aug2023
mrb g sbndaq_artdaq_core@feature/update_Aug2023
mrb g sbncode@v09_75_03_02
mrb g icarusalg@v09_75_03_02
mrb g icaruscode@v09_75_03_02
```
Here, `feature/update_Aug2023` is the name of a branch in the `sbndqm`-related repositories that has needed updates. `v09_75_03_02` is the tag in the other offline repositories that points to the stable release (at those version numbers), in this case for ICARUS. Oftentimes it may be necessary to pull down and rebuild offline code (even if it hasn't changed) in order to get properly updated dependencies: in this case, a dependency on `sbndaq_artdaq_core`. In many cases however, you may only need one branch (like `sbndqm`).

### Development in Online Machine

#### Generic Development Area Setup
To setup a development environment in an online machine (like `icarus-evb01`, `sbn-daq01`):
```
source /daq/software/products/setup

setup mrb
export MRB_PROJECT=sbndqm

mkdir <your_new_dev_area>
cd <your_new_dev_area>
mrb newDev -v v1_02_00 -q e20:prof #replace with your desired sbndqm version here!
source localProducts_sbndqm_*/setup 

cd srcs/
mrb g sbndqm
cd $MRB_BUILDDIR
mrbsetenv
mrb i -j8
```

#### Newest Development Area Setup
The latest SBNDQM version, the one currently in use in SBND, is v1_03_00.
```bash
cd DQM_DevAreas/
source /daq/software/products/setup
setup mrb
export MRB_PROJECT=sbndqm
mkdir your_dev_area
cd your_dev_area/
mrb newDev -v v1_03_00 -q e26:prof
source localProducts_sbndqm_v1_03_00_e26_prof/setup
cd srcs/
mrb g sbndaq_online@develop # or mrb g -t v1_01_00 sbndaq_online
mrb g sbndqm@release/v1_04_00 #feature/SBND-v1_04_01
cd $MRB_BUILDDIR
mrbsetenv
mrb i -j8
mrbslp
```

To run the SBND DQM, there is a dependency on sbndcode:
```bash
setup sbndcode -v v09_93_01_02 -q e26:prof #for evd
```

### Using your local build

When you then build in the future, you just need to source the products area (`source` commands above) and then do:
```
cd <your_dev_area>
setup mrb
source localProducts_sbndqm_*/setup
mrbsetenv
mrb i -j8
```

#### Source Online sbndqm v1_03_00 Dev Area
``` shell
source /daq/software/products/setup
setup mrb
source localProducts*/setup
mrbsetenv
mrbsetenv
setup sbndcode -v v09_93_01_02 -q e26:prof
```

### Start Redis Database

How to start the redis on sbnd-db01:

ssh sbnd-db01

source /software/products/setup


source /home/nfs/sbnddqm/start_redis

Release Instructions
----------------------------------------------
[See here for release instructions for online-related software](ReleaseInstructions)

Old wiki
----------------------------------------------
Please
see the old wiki for a lot of historical detail.

[Old redmine wiki](https://cdcvs.fnal.gov/redmine/projects/sbndqm/wiki).

# Useful Links
* git info: [Github guides](https://guides.github.com/)
* [Older instructions on Github Migration](GithubMigration.md)


# Troubleshooting
----------------------------------------------
The stars have to be aligned for the DQM to work properly; a lot can go wrong. 

## Common "Easy" Checks:
- The DQM and DAQ have to be running on the same machine, e.g. sbnd-evb04
- Make sure redis database is on

## If it's still not working...
- Check your log files, if they exist. Or your terminal output if you try running your online monitoring script from the terminal. It often gives an output that can aid in debugging

## Solutions to Larger Issues:

### SharedMemoryManager Issue:
Oftentimes, there will be an issue that looks like the following:
```
%MSG-e SharedMemoryManager:  Early 12-Mar-2024 10:33:04 CDT JobSetup SharedMemoryManager.cc:280
Failed to connect to shared memory segment with key 0xee011f62, errno=2 (No such file or directory).  Please check if a stale shared memory segment needs to be cleaned up. (ipcs, ipcrm -m <segId>)
```
This occurs when 



# Contributing to this wiki
----------------------------------------------


The content of this wiki is tracked in a GitHub repository [SBNSoftware/SBNSoftware.github.io](https://github.com/SBNSoftware/SBNSoftware.github.io)
under the
[`sbndaq_wiki`](https://github.com/SBNSoftware/SBNSoftware.github.io/tree/master/sbndaq_wiki)
subdirectory. Some details using this particular theme can be found [here](https://github.com/chrisrhymes/bulma-clean-theme).
