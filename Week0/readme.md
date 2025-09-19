# Week0 – Tool Installation 🚀

**Prepared by:** Omkar  

This document shows the installation and verification of all tools required in Week0.  
Screenshots are available in the `images/` folder as proof of successful setup.  

---

## 📌 Tools Covered
- Yosys (Digital synthesis)
- Icarus Verilog (HDL simulation)
- GTKWave (Waveform viewing)
- NGSpice (Analog circuit simulation)
- Magic VLSI (Layout design)

---

## 🔧 System Requirements
- **OS:** Ubuntu 20.04+ (VirtualBox recommended for Windows/Mac users)  
- **RAM:** 6 GB minimum  
- **Disk:** 50 GB free  
- **CPU:** 4 vCPUs  

---

## 🛠 Installation & Verification

### 1. Yosys – *Synthesis tool*
Why required: Converts RTL (Verilog) code into gate-level netlists.  

```bash
$ sudo apt-get update
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys
$ sudo apt install make               # If make is not installed
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make config-gcc
# Yosys build depends on a Git submodule called abc, which hasn't been initialized yet. You need to run the following command before running make
$ git submodule update --init --recursive
$ make 
$ sudo make install
```
### Install result: 

