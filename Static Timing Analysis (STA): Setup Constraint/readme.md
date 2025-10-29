# ⏳ Static Timing Analysis (STA): Setup Constraint

This document illustrates the fundamental timing relationship between two sequential elements (flip-flops) in a synchronous digital circuit, focusing specifically on the **Setup Analysis** for a common Register-to-Register (R2R) path. This analysis is critical in ensuring the digital design functions reliably at its intended clock frequency.

---


<img width="1312" height="650" alt="image" src="https://github.com/user-attachments/assets/5eea539d-3f9b-413d-b137-1c14b71c0639" />

---

## 1. ⚙️ Circuit Components and Clock Timing

The diagram models a basic Register-to-Register ($\text{R2R}$) path, which is the core pipeline stage in a chip.

* **Launch Flop (Source):** The flip-flop (FF) whose output ($\text{Q}$) changes and **launches** the data signal into the combinational logic.
* **Capture Flop (Destination):** The flip-flop that **captures** the data at its data pin ($\text{D}$) on the next clock edge.
* **Combinational Logic (Cloud, $\Theta$):** The block of logic gates that processes the data. Its delay is represented by $\mathbf{\Theta}$.

### Nominal Clock Timing

The clock signal ($\text{CLK}$) defines the time budget for the data path:

* **Frequency (F):** $1\text{GHz}$ (GigaHertz).
* **Period (T):** $1/\text{F} = 1\text{ns}$ (nanosecond). This is the nominal time the data has to travel.

---

## 2. 🕰️ Clock Propagation and Skew

The clock signal is not ideal; it takes time to travel from the clock source to each flip-flop. This difference in arrival times is called **skew**.

| Term | Symbol | Description |
| :--- | :--- | :--- |
| **Launch Clock Arrival** | $\mathbf{\Delta_1}$ | The time it takes the clock to arrive at the Launch Flop's clock pin. |
| **Capture Clock Arrival** | $\mathbf{\Delta_2}$ | The time it takes the clock to arrive at the Capture Flop's clock pin relative to the ideal time $\text{T}$. |
| **Skew** | $\mathbf{|\Delta_1 - \Delta_2|}$ | The difference in arrival time of the same clock edge at the related launch and capture flops. This directly impacts the available time for the data path. |

---

## 3. ✅ The Setup Timing Constraint

The **Setup Constraint** ensures that the data arrives at the Capture Flop's $\text{D}$ pin before the capture clock edge, allowing the flop sufficient time ($\text{T}_{\text{setup}}$) to reliably capture the data.

### Data Arrival Time (DAT)

This is the total time the data takes to travel from the clock edge at the Launch Flop to the $\text{D}$ pin of the Capture Flop.

$$\mathbf{\text{DAT}} = \Delta_1 + \text{T}_{\text{CLK} \rightarrow \text{Q}} + \Theta$$

* $\text{T}_{\text{CLK} \rightarrow \text{Q}}$ is the delay of the Launch Flop.
* $\Theta$ is the combinational delay.

### Data Required Time (DRT)

This is the time by which the data must arrive to meet the next clock edge at the Capture Flop, taking the flop's required setup time into account.

$$\mathbf{\text{DRT}} = (\text{T} + \Delta_2) - \text{T}_{\text{setup}}$$

### The Setup Constraint Inequality

The critical constraint for a successful setup check is:

$$\text{Data Arrival Time} < \text{Data Required Time}$$

* **Simplified Inequality (as shown in the diagram for visual clarity):**

$$\mathbf{(\Theta + \Delta_1) < (\text{T} + \Delta_2)}$$

**Meaning:** The time it takes for the data to be launched ($\Delta_1$) and travel across the logic ($\Theta$) must be less than the time available up to the capture clock edge ($\text{T} + \Delta_2$). If this condition is met, the path passes the setup check.
