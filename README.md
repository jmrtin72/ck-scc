## Collective Knowledge workflow for the Student Cluster Competition (SCC)

[![compatibility](https://github.com/ctuning/ck-guide-images/blob/master/ck-compatible.svg)](https://github.com/ctuning/ck)
[![automation](https://github.com/ctuning/ck-guide-images/blob/master/ck-artifact-automated-and-reusable.svg)](https://ReproIndex.com)
[![workflow](https://github.com/ctuning/ck-guide-images/blob/master/ck-workflow.svg)](https://cKnowledge.org)
[![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)

## Introduction

This repository contains an evolving [Collective Knowledge](https://cKnowledge.org) 
workflow to standardize the preparation, execution and validation of submissions
(Digital Artifacts) for the [Student Cluster Competition Reproducibility Challenge](http://www.studentclustercompetition.us/)

## CK installation

You need to install the Collective Knowledge framework (CK) as described 
[here](https://github.com/ctuning/ck#Installation). 

CK is a community project to share and reuse automation tasks in the form 
of [Python actions with Unique ID, JSON meta description and standardized API](https://reproindex.com/components/&c=module). 
For example, you can see all Python actions for this SCC workflow [here](https://github.com/reproindex/ck-scc/blob/master/module/scc-workflow/module.py).

CK was designed to be very small and portable: 
CK only requires Python 2.7 or 3+, git and wget, 
can run natively on practically any system, and complements many existing DevOps tools.
If you encounter a problem during installation, do not hesitate 
to submit a [GitHub ticket](https://github.com/ctuning/ck/issues)
or ask for help using the [CK Slack channel](https://bit.ly/ck-slack) 
or [CK Google group](https://bit.ly/ck-google-group).

If you have never used CK, we also suggest you to check 
this [blog article](https://michel.steuwer.info/About-CK) and
the [CK getting started guide](https://github.com/ctuning/ck/wiki/First-Steps).

## SCC workflow installation

You need to install this repository to be able to reuse CK-SCC automation actions as follows:

```
$ ck pull repo --url=https://github.com/reproindex/ck-scc
```

## Creating a dummy CK repository for your Digital Artifact

We assume that you were already assigned a team number {TN}. 
You can create a dummy CK repository for your artifacts as follows:

```
$ ck prepare scc-workflow
```

CK will ask you about the year of the SCC competition {YEAR} and your team number {TEAM}.
It will then create a CK repository "scc-{YEAR}-{TEAM}"
with a CK entry "scc-workflow:{YEAR}-{TEAM}" to keep your Digital Artifact.
This entry will already have a directory structure required 
for your artifact submission (taken from the CK entry 
"[scc-workflow:template](https://github.com/reproindex/ck-scc/tree/master/scc-workflow/template)").

For example, if your team number is 2 and the competition year is 2019, 
CK will create repo:scc-2019-2 with an entry scc-workflow:2019-2:

```
$ ck ls repo:scc*

 scc-2019-2

$ ls -a `ck find scc-workflow:2019-2`

 .  ..  .cm  ReproducibilityChallenge

$ ls -a `ck find scc-workflow:2019-2`/ReproducibilityChallenge

 .  ..  compile  doc  figures  run

```

## Installing dependencies

You should go to the above directory with your digital artifact and 
provide commands required to install all dependencies
for the SCC application on your machine in the following script:
```
ReproducibilityChallenge/compile/install-deps.sh
```

You and other users will be able to run this script via CK using the following CK action:
```
$ ck install_deps scc-workflow
```

You should also describe how to install all dependencies in the following ReadMe file:
```
ReproducibilityChallenge/compile/README
```

## Compiling application

You should go to the above directory with your digital artifact and 
provide all commands required to compiler the SCC application
on your machine in the following script:
```
ReproducibilityChallenge/compile/install-deps.sh
```

You and other users will be able to run this script via CK using the following CK action:
```
$ ck install_deps scc-workflow
```

You should also provide compilation instructions in the following ReadMe file:
```
ReproducibilityChallenge/compile/README
```

## Downloading input

You should go to the CK directory of your digital artifact and 
check/update all commands required to download all input files
for the SCC application in the following script:
```
ReproducibilityChallenge/run/scripts/download-data.sh
```

You and other users will be able to run this script via CK using the following CK action:
```
$ ck download_data scc-workflow
```

You should also describe how to download data in the following ReadMe file:
```
ReproducibilityChallenge/run/scripts/README
```

## Running application

You should go to the CK directory of your digital artifact and 
add all commands required to run the SCC application
in the following script:
```
ReproducibilityChallenge/run/scripts/run.sh
```

You and other users will be able to run this script via CK using the following CK action:
```
$ ck run_analysis scc-workflow
```

You should also describe how to run the SCC application in the following ReadMe file:
```
ReproducibilityChallenge/run/scripts/README
```

## Post processing and validating results

You should go to the CK directory of your digital artifact and 
add all commands required to post process and validate the results
of the SCC application in the following script:
```
ReproducibilityChallenge/run/scripts/post-process.sh
```

You and other users will be able to run this script via CK using the following CK action:
```
$ ck post_process scc-workflow
```

You should also describe how to run the SCC application in the following ReadMe file:
```
ReproducibilityChallenge/run/scripts/README
```

## Plotting graphs

You should go to the CK directory of your digital artifact and 
add all commands required to plot figures for the SCC application
in the following script:
```
ReproducibilityChallenge/figures/scripts/plot.sh
```

You and other users will be able to run this script via CK using the following CK action:
```
$ ck plot scc-workflow
```

You should also describe how to plot graphs in the following ReadMe file:
```
ReproducibilityChallenge/figures/scripts/README
```

## Packing your Digital Artifact

You can pack your Digital artifact as follows:
```
$ ck pack scc-workflow:{YEAR}-{TEAM}
```

The file "scc-{YEAR}-{TEAM}.zip" with your Digital Artifact will be created in your current directory.

## Packing the CK repository with your Digital Artifact

You can also pack and share the whole CK repository with your Digital Artifact:

```
$  ck zip repo:scc-{YEAR}-{TEAM} 
```

In such case, it will be easier for evaluators or users to unpack and test it in standard way via CK as follows:
```
$ ck add repo --zip=ckr-scc-2019-{TN}.zip --quiet
```

## Extra notes

* You can run all above actions (install_deps, compile, download_data, run_analysis, post_process and plot) using CK "run" action as follows:
```
$ ck run scc-workflow
```

* This CK repository depends on another CK repository: [ck-env](https://reproindex.com/components/4adfaff6d69d41a9:1ff43ae88715a8c1).
  This dependency is described in the [.ckr.json](https://github.com/reproindex/ck-scc/blob/master/.ckr.json#L9) file.

## Future work

We plan to add [automatic detection](https://ReproIndex.com/components/&c=soft) of required software, models and data sets,
[installation of missing packages](https://ReproIndex.com/components/&c=package), unified benchmarking,
and experiment reply based on the [SCC'18 CK workflow](https://github.com/ctuning/ck-scc18).
We also plan to automate visualization and comparison of results 
via [CK dashboards](https://cKnowledge.org/dashboard).
Feel free to send your own patches with enhancements for this workflow!

## Feedback 

If you have questions or suggestions, do not hesitate to contact us via 
our [open discussion group](https://groups.google.com/forum/#!forum/collective-knowledge) 
or the [CK Slack channel](http://bit.ly/ck-slack).
