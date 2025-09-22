# Day-1 — Introduction to Verilog RTL Design & Synthesis 🚀

Welcome to **Day-1 of the RTL Design & Synthesis workshop!**  
This session introduces you to **simulation and synthesis** using open-source tools like **Icarus Verilog**, **Yosys**, and **ABC**, with practical hands-on labs.

---

## 📑 Table of Contents
- [1. What is a Simulator, Design, and Testbench?](#1-what-is-a-simulator-design-and-testbench)
- [2. Getting Started with iverilog](#2-getting-started-with-iverilog)
- [3. Lab: Simulating a 2-to-1 Multiplexer](#3-lab--simulating-a-2-to-1-multiplexer)
- [4. Verilog Code — Analysis](#4-verilog-code--analysis)
- [5. Introduction to Yosys & Gate Libraries](#5-introduction-to-yosys--gate-libraries-sky130-example)
- [6. Summary](#6-summary)



---

## 1. What is a Simulator, Design, and Testbench?

- **Design (RTL):** Verilog code describing hardware behavior at Register-Transfer Level (RTL).  
  *Example:* `good_mux.v`  

- **Testbench (TB):** A Verilog module that instantiates the design, applies stimulus, and records waveforms.  
  *Example:* `tb_good_mux.v`  

- **Simulator:** Software tool that runs the **design + testbench**, producing results and waveforms.  

**Tools Used:**
- `iverilog` → compile Verilog files  
- `./a.out` → run simulation  
- `gtkwave` → view waveforms (.vcd files)  
<img width="700" height="700" alt="testbench" src="https://github.com/user-attachments/assets/0d0d8a14-cc9d-44ee-9dab-f8b19694e859" />

---

## 2. Getting Started with iverilog

**Setup your workspace:**
```bash
# Create workspace
mkdir VSD
cd VSD

# Clone the workshop repo
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
cd sky130RTLDesignAndSynthesisWorkshop # change directry 
```

**Explore the directories:**
``` bash
cd lib            # contains sky130 library (.lib files)
cd my_lib         # custom libraries
cd verilog_files  # RTL design & TBs
```

**Below is the flow graph of iverilog working**
<img width="700" height="700" alt="iverilog_flow" src="https://github.com/user-attachments/assets/f8e6458c-f0a8-4830-b80f-937d5e3ad3fb" />

---

## 3. Lab — Simulating a 2-to-1 Multiplexer
**RTL Code:** good_mux.v
``` bash
module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
    if(sel)
        y <= i1;
    else 
        y <= i0;
end
endmodule
```
**Testbench: tb_good_mux.v**
``` bash
`timescale 1ns / 1ps
module tb_good_mux;
    reg i0, i1, sel;
    wire y;

    good_mux uut (.sel(sel), .i0(i0), .i1(i1), .y(y));

    initial begin
        $dumpfile("tb_good_mux.vcd");   // create VCD file for waveform
        $dumpvars(0,tb_good_mux);       // dump all signals of testbench
        sel = 0; i0 = 0; i1 = 0;        // initialize inputs
        #300 $finish;                   // stop simulation after 300 ns
    end

    always #75 sel = ~sel;  // toggle sel every 75 ns
    always #10 i0 = ~i0;    // toggle i0 every 10 ns
    always #55 i1 = ~i1;    // toggle i1 every 55 ns
endmodule
```

**Compile & Run:**
``` bash
cd verilog_files
iverilog good_mux.v tb_good_mux.v   # compile RTL + testbench
./a.out                             # run simulation and generate VCD file
```

**View waveform in GTKWave:**
``` bash
gtkwave tb_good_mux.vcd
```
**Output from GTKWave :**
<img width="1632" height="927" alt="gtkwave" src="https://github.com/user-attachments/assets/4663fc8d-900a-4f05-86c3-d421fe26346a" />



---
## 4. Verilog Code — Analysis
**good_mux.v (Design)**

- Declares inputs i0, i1, sel, and output y.

- **always @(*)** → executes whenever inputs change.

- If sel=1, output y follows i1; otherwise y follows i0.
  
➡ **Implements a 2:1 Multiplexer**.

**tb_good_mux.v (Testbench)**

- Instantiates the mux.

- Uses **$dumpfile and $dumpvars** to record signals into tb_good_mux.vcd.

- Stimuli applied:

- sel toggles every **75 ns**

- i0 toggles every **10 ns**

- i1 toggles every **55 ns**

- Simulation ends at **300 ns.**

➡ **Generates enough transitions to observe all input/output cases in GTKWave.**

---

## 5. Introduction to Yosys & Gate Libraries (sky130 example)

- **Yosys** is an open-source synthesis tool.
- We use the **Sky130 standard cell library** (sky130_fd_sc_hd__tt_025C_1v80.lib) to map RTL → gate-level netlist.



### Synthesis Lab with Yosys + ABC

Start Yosys:
``` bash
yosys
```

Inside Yosys:
```bash
# Load standard cell library
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

# Read RTL
read_verilog good_mux.v

# Run synthesis
synth -top good_mux

# Technology mapping using ABC
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

# Show schematic (Graphviz/X display needed)
show

# Write synthesized netlist
write_verilog good_verilog_netlist.v

# (Optional) Open in editor
!gvim good_verilog_netlist.v
```

**View using 'show' command :**

<img width="700" height="700" alt="netlist image" src="https://github.com/user-attachments/assets/f29a277e-c76e-48bc-8722-db052e80f3f0" />


**🔑 Command Explanations:**

- **read_liberty -lib** → load timing/power library of cells
- **read_verilog** → load your design RTL
- **synth -top** → synthesize design with specified top module
- **abc** -liberty → map design to actual cells in .lib
- **show** → schematic view
- **write_verilog** → export synthesized gate-level netlist

---

## 6. Summary 

✔ **Simulated RTL with iverilog → produced .vcd → viewed in gtkwave**

✔ **Synthesized RTL with Yosys + ABC → mapped to sky130 standard cells**

