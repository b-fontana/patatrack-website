---
title: "Patatrack Releases"
author: "Andrea Bocci"
layout: wiki
resource: true
categories: wiki
activity:  instructions
---

## Installing "Patatrack" CMSSW releases
The current Patatrack development branch is based on `CMSSW_11_0_X`, and supports CUDA 10.1 and GCC 8.3.x.

While it is possible to start from the underlying vanilla CMSSW relese, using a dedicated release has few advantages:
 - drop optimised support for SM 6.1 to speed up the build time;
 - include the changes from the "Patatrack" development branch.

`CMSSW_10_0_0_pre11_Patatrack` is available for the architecture(s)
 - `slc7_amd64_gcc820`.

On **vinavx2** and other machines the releases are nstalled under `/data/cmssw/`.

On **cmg-gpu1080** the releases are available installed under `/data/patatrack/cmssw/`.


### Bootstrap a local installation of CMSSW
Choose for `VO_CMS_SW_DIR` a directory to which you have write permissions, and
has at least 20 GB of spare disk space. **Do not** use a directory on EOS.

The following instructions assume the `slc7_amd64_gcc820` architecture; to use a
different one simply replace the desired architecture.

```bash
cd <...>

export LANG=C
export VO_CMS_SW_DIR=$PWD
export SCRAM_ARCH=slc7_amd64_gcc820

wget http://cmsrep.cern.ch/cmssw/bootstrap.sh -O $VO_CMS_SW_DIR/bootstrap.sh
chmod a+x $VO_CMS_SW_DIR/bootstrap.sh
$VO_CMS_SW_DIR/bootstrap.sh -a $SCRAM_ARCH -r cms -path $VO_CMS_SW_DIR setup
```

### Updating a local installation of CMSSW
After the initial boostrap, the same directory can be used to install new releases.

It is recommended to update `cmspkg` itself on a regular basis:
```bash
cd <...>

export LANG=C
export VO_CMS_SW_DIR=$PWD
export SCRAM_ARCH=slc7_amd64_gcc820

$VO_CMS_SW_DIR/common/cmspkg -a $SCRAM_ARCH upgrade -y
```


## `CMSSW_11_0_X_Patatrack` development branch

### Prerequisite: install `CMSSW_11_0_0_pre11` and its dependencies
Most of the externals for `CMSSW_11_0_0_pre11_Patatrack` need to be installed from the
official repository; the easiest approach is to install them automatically
together with `CMSSW_11_0_0_pre11`:
```bash
$VO_CMS_SW_DIR/common/cmspkg -a $SCRAM_ARCH install -y cms+cmssw+CMSSW_11_0_0_pre11
```

### Install `CMSSW_11_0_0_pre11_Patatrack`
Patatrack releases can be installed with `cmspkg`, using the dedicated repository
"cms.patatrack":
```bash
$VO_CMS_SW_DIR/common/cmspkg -a $SCRAM_ARCH -r cms.patatrack install -y cms+cmssw+CMSSW_11_0_0_pre11_Patatrack
```
