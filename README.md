# Intel:registered: Data Center Platform Overlay for Linux* OS

This repository contains prototype code for testing hardware feature enablement on Intel’s upcoming Intel’s next generation Xeon server code named Eagle Stream / Sapphire Rapids. This will be published and updated till CPU launch complete and is not planned to be supported beyond that. This code is to be used as reference. For support and certification use your own distribution vendors. 

Note: The code base includes enablement for Sapphire Rapids features except Quick Assist Technology, Ethernet drivers, Volume Management Device (VMD) & 
Intel® Virtual RAID on CPU (VROC) 

## Reporting Issues
Use github issues for questions: https://github.com/intel/dcp-overlay/issues 

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

All packages sources are available as Source RPMs in [published repository](https://download.01.org/dcp-overlay/repo/src).


## Release notes 
### 0.4.20.0-2 
This is the first public overlay release to support Intel EagleStream / Sapphire Rapids Platform. 

If deploying Intel:registered: Data Streaming Accelerator with this prototype code, use the following:

Driver_name attribute for wq: It can be configured from the following list: crypto, dmaengine, mdev and user. Take user for example, if use config file add ``driver_name:user`` in work queue configuration. If use ``accel-config config-wq``, add ``-d user`` or ``–driver-name=user`` 

If deploying Intel:registered: Trusted Domain Extensions (Intel:registered: TDX) feature with this prototype code, use the following:
1. “tdx_host=on” must be appended to host kernel command line parameter, otherwise Intel:registered: TDX will not be initialized 
2. TD guest cannot launch, qemu error “qemu-kvm: KVM_TDX_INIT_VM failed: Operation not supported” - Disable CET and Arch LBR with adding " -arch-lbr,-shstk " to qemu parameter to create TDs (Arch LBR is not supported in TD, and CET has not been fully tested in TD, so suggest disable them before TD guest launch) 
3. A ``tdx_disable_filter`` entry has been added to the kernel command line 
4. Disable NUMA balancing in host, 
```echo 0 > /proc/sys/kernel/numa_balancing``` 

---

COPYRIGHT © 2022 INTEL CORPORATION. ALL RIGHTS RESERVED

*[OTHER NAMES AND BRANDS MAY BE CLAIMED AS THE PROPERTY OF OTHERS](https://www.intel.com/content/www/us/en/legal/trademarks.html "Trademarks")
