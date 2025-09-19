# Week0 – Tool Installation 🚀

**Prepared by:** **Omkar**   

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
- **OS:**  *Ubuntu 20.04+ (VirtualBox recommended for Windows/Mac users)*  
- **RAM:**   *6 GB minimum* 
- **Disk:**  *50 GB free*  
- **CPU:**  *4 vCPUs*  

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
![Image](https://github.com/user-attachments/assets/c25bb647-6f72-4473-8a5b-e3a0cd449840)
---

### 2.Icarus Verilog (iverilog) – HDL simulator
Why required: Used to simulate Verilog designs before synthesis.

```bash
sudo apt-get update
sudo apt-get install -y iverilog
```
### Install result: 
![Image](https://github.com/user-attachments/assets/9cfbe190-ddb9-4781-a05d-d50d200d26dd)

---

### 3. GTKWave – Waveform viewer
Why required: Displays simulation results (waveforms) from Verilog/Spice outputs.
```bash
sudo apt-get update
sudo apt-get install -y gtkwave
```

### Install result: 
![Image](https://github.com/user-attachments/assets/743d4634-d25f-49db-ab7d-907e2830c588)
---

### 4. NGSpice – Analog circuit simulator

Why required: Used to analyze and verify analog/mixed-signal circuits.
``` bash
sudo apt-get update
sudo apt-get install -y ngspice
```
If turball needed then follow below steps;
```bash
$ tar -zxvf ngspice-37.tar.gz
$ cd ngspice-37
$ mkdir release
$ cd release
$ ../configure --with-x --with-readline=yes --disable-debug
$ make
$ sudo make install 

```

### Install result: 
![Image](https://github.com/user-attachments/assets/3471398a-aa4c-4d95-bcb0-95f0ca76f739)
---

### 5. Magic VLSI – Layout editor

Why required: Used for designing and viewing IC layouts in VLSI flow.
```bash
$ sudo apt-get install m4
$ sudo apt-get install tcsh
$ sudo apt-get install csh
$ sudo apt-get install libx11-dev
$ sudo apt-get install tcl-dev tk-dev
$ sudo apt-get install libcairo2-dev
$ sudo apt-get install mesa-common-dev libglu1-mesa-dev
$ sudo apt-get install libncurses-dev
git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
make
sudo make install
```
If not try the below one :
``` bash
sudo apt-get update
sudo apt-get install -y magic
```
### Install result: 
![Image](https://github.com/user-attachments/assets/97ca8540-12b0-4d3b-af97-4d532d5be05b)
![Image](https://github.com/user-attachments/assets/8331e2ca-0026-41d3-b8ee-ee38b1641f43)
---

### ✅ Final Note

### With these tools installed, both digital (RTL → synthesis → simulation → waveforms) and analog/layout (SPICE + VLSI design) workflows are supported
---
