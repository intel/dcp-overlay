# Intel:registered: Data Center Platform Overlay for Linux* OS

This repository contains prototype code for testing hardware feature enablement on Intel’s upcoming Intel’s next generation Xeon server code named Eagle Stream / Sapphire Rapids. This will be published and updated till CPU launch complete and is not planned to be supported beyond that. This code is to be used as reference. For support and certification use your own distribution vendors. 

Use github issues for questions: https://github.com/intel/dcp-overlay/issues 

Note: The code base includes enablement for Sapphire Rapids features except Quick Assist Technology, Ethernet drivers, Volume Management Device (VMD) & 
Intel® Virtual RAID on CPU (VROC) 

## Prerequisites 

The system under test should have a fully working CentOS Stream 8 installation. 
As the Data Center Platform Overlay targets Eagle Stream / Sapphire Rapids platforms, this should be the underlying hardware to fully support all the included features. 

## Install 

Add the "Intel:registered: Data Center Platform Overlay for Linux* OS" repository to your distribution.

Download and add the repository file to the operating system:
```
curl -O https://download.01.org//dcp-overlay/Intel-DCP-Overlay.repo 
sudo mv Intel-DCP-Overlay.repo /etc/yum.repos.d/Cancel changes
```

Install the set of overlay packages:
```
sudo dnf groupinstall dcp-overlay
```

Remove the existing ``rpcgen`` package if installed due to a possible conflict:
```
sudo dnf remove rpcgen
```

Update to the latest releases:
```
sudo dnf update --allowerasing
```
Note: ``--allowerasing`` is required to resolve a minor conflict the the provided ``glibc`` package.

## Linux Kernel Full Sources Repository

The full Linux Kernel source are availble at https://github.com/intel/linux-kernel-dcp

All packages sources are available as Source RPMs in [published repository](https://download.01.org/dcp-overlay/repo).


## 0.4.20.0-2 Public Release notes 

...

---

COPYRIGHT © 2022 INTEL CORPORATION. ALL RIGHTS RESERVED

*[OTHER NAMES AND BRANDS MAY BE CLAIMED AS THE PROPERTY OF OTHERS](https://www.intel.com/content/www/us/en/legal/trademarks.html "Trademarks")
