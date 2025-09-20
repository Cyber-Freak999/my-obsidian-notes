# a 30MVA, 11KV generator has a sequence impedance of Z_1=Z_2=j0.2 pu. Assuming the generator is operating at no load and rated value when a line to line bolted fault occurs at the generator terminals, find the actual value of the line currents and the per unit value of line to neutral voltages under fault conditions

This analysis uses the method of symmetrical components, assuming the generator is initially operating at $1.0$ per unit (pu) voltage (rated value at no load) and neglecting resistance, which is common practice for fault calculations. Since the fault is at the terminals of an unloaded machine, the internal voltage $E_a$ is equal to the prefault terminal voltage $V_f$, which is assumed to be $\mathbf{1.0 \angle 0^\circ \text{ pu}}$.

The given data is:

- Base MVA ($S_B$): 30 MVA
- Base Line-to-Line kV ($V_{B, LL}$): 11 kV
- Sequence Impedances: $Z_1 = Z_2 = j0.2$ pu.
- Fault Type: Line-to-Line (L-L) bolted fault ($Z_f = 0$) between phases $b$ and $c$.

### 1. Calculation of Base Quantities

We must first determine the base current to convert the per unit fault currents to actual ampere values:

$$\text{Base Current } (I_B) = \frac{S_B}{\sqrt{3} V_{B, LL}}$$ $$I_B = \frac{30,000 \text{ kVA}}{\sqrt{3} \times 11 \text{ kV}} \approx \mathbf{1574.57 \text{ A}}$$

### 2. Per Unit Fault Current Calculation

For a line-to-line fault between phases $b$ and $c$, the zero-sequence current $I_{a0}$ is zero, and the positive and negative sequence networks are connected in series opposition. The positive sequence current $I_{a1}$ is calculated as:

$$\mathbf{I_{a1}} = \frac{\mathbf{E_a}}{Z_1 + Z_2}$$

Where $E_a = 1.0 \angle 0^\circ$ pu (prefault internal voltage):

$$\mathbf{I_{a1}} = \frac{1.0 \angle 0^\circ}{j0.2 + j0.2} = \frac{1.0}{j0.4} = -j2.5 \text{ pu}$$ $$\mathbf{I_{a2}} = -\mathbf{I_{a1}} = j2.5 \text{ pu}$$ $$\mathbf{I_{a0}} = 0 \text{ pu}$$

#### Line Currents (Per Unit):

The phase currents are determined using the symmetrical component transformation: $$\mathbf{I_a} = \mathbf{I_{a0}} + \mathbf{I_{a1}} + \mathbf{I_{a2}}$$ $$\mathbf{I_b} = \mathbf{I_{a0}} + a^2 \mathbf{I_{a1}} + a \mathbf{I_{a2}}$$ $$\mathbf{I_c} = \mathbf{I_{a0}} + a \mathbf{I_{a1}} + a^2 \mathbf{I_{a2}}$$

1. **Current $I_a$:** $$\mathbf{I_a} = 0 + (-j2.5) + (j2.5) = \mathbf{0 \text{ pu}}$$ (This confirms the L-L fault condition $I_a = 0$).
    
2. **Current $I_b$ (Fault Current magnitude):** Using the derived relation for L-L faults ($\mathbf{I_b} = (a^2 - a)\mathbf{I_{a1}}$): $$\mathbf{I_b} = (-j\sqrt{3}) (-j2.5) = -\sqrt{3} \times 2.5$$ $$\mathbf{I_b} \approx \mathbf{-4.3301 \text{ pu}} \quad \text{or} \quad \mathbf{4.3301 \angle 180^\circ \text{ pu}}$$
    
3. **Current $I_c$:** For a bolted L-L fault between $b$ and $c$, $\mathbf{I_c} = -\mathbf{I_b}$. $$\mathbf{I_c} \approx \mathbf{4.3301 \text{ pu}} \quad \text{or} \quad \mathbf{4.3301 \angle 0^\circ \text{ pu}}$$
    

### 3. Actual Value of Line Currents

The actual RMS line currents are found by multiplying the per unit magnitudes by the base current $I_B$:

|Current|Per Unit Value|Actual Value (A)|
|:-:|:-:|:-:|
|$\mathbf{I_a}$|0 pu|**0 A**|
|$\mathbf{I_b}$|$4.3301 \angle 180^\circ$ pu|$4.3301 \times 1574.57 \text{ A} \approx \mathbf{6820.7 \text{ A}}$|
|$\mathbf{I_c}$|$4.3301 \angle 0^\circ$ pu|$4.3301 \times 1574.57 \text{ A} \approx \mathbf{6820.7 \text{ A}}$|

### 4. Per Unit Value of Line-to-Neutral Voltages During Fault

The line-to-neutral voltages at the generator terminals ($\mathbf{V_a}, \mathbf{V_b}, \mathbf{V_c}$) are determined by first finding the sequence voltages ($\mathbf{V_{a0}}, \mathbf{V_{a1}}, \mathbf{V_{a2}}$) at the fault point (terminals):

$$\mathbf{V_{a1}} = \mathbf{E_a} - \mathbf{I_{a1}} Z_1$$ $$\mathbf{V_{a2}} = 0 - \mathbf{I_{a2}} Z_2$$ $$\mathbf{V_{a0}} = 0$$

1. **Positive Sequence Voltage $\mathbf{V_{a1}}$:** $$\mathbf{V_{a1}} = 1.0 \angle 0^\circ - (-j2.5) (j0.2) = 1.0 - 0.5 = \mathbf{0.5 \text{ pu}}$$
    
2. **Negative Sequence Voltage $\mathbf{V_{a2}}$:** $$\mathbf{V_{a2}} = - (j2.5) (j0.2) = - (-0.5) = \mathbf{0.5 \text{ pu}}$$
    
3. **Zero Sequence Voltage $\mathbf{V_{a0}}$:** $$\mathbf{V_{a0}} = \mathbf{0 \text{ pu}}$$
    

#### Line-to-Neutral Voltages (Per Unit):

The phase voltages are found by summing the sequence voltages:

1. **Voltage $\mathbf{V_a}$:** $$\mathbf{V_a} = \mathbf{V_{a0}} + \mathbf{V_{a1}} + \mathbf{V_{a2}} = 0 + 0.5 + 0.5 = \mathbf{1.0 \text{ pu}}$$
    
2. **Voltage $\mathbf{V_b}$:** $$\mathbf{V_b} = \mathbf{V_{a0}} + a^2 \mathbf{V_{a1}} + a \mathbf{V_{a2}}$$ Since $V_{a1} = V_{a2} = 0.5 \text{ pu}$: $$\mathbf{V_b} = 0.5 (a^2 + a)$$ Knowing that $a^2 + a = -1$: $$\mathbf{V_b} = 0.5 (-1) = \mathbf{-0.5 \text{ pu}}$$
    
3. **Voltage $\mathbf{V_c}$:** $$\mathbf{V_c} = \mathbf{V_{a0}} + a \mathbf{V_{a1}} + a^2 \mathbf{V_{a2}}$$ $$\mathbf{V_c} = 0.5 (a + a^2) = \mathbf{-0.5 \text{ pu}}$$
    

|Phase|Per Unit Voltage (Line-to-Neutral)|
|:-:|:-:|
|$\mathbf{V_a}$|$\mathbf{1.0 \angle 0^\circ \text{ pu}}$|
|$\mathbf{V_b}$|$\mathbf{-0.5 \text{ pu}}$ (or $0.5 \angle 180^\circ \text{ pu}$)|
|$\mathbf{V_c}$|$\mathbf{-0.5 \text{ pu}}$ (or $0.5 \angle 180^\circ \text{ pu}$)|

_(Note: The condition for an L-L bolted fault between $b$ and $c$ is $V_b = V_c$ and $V_b - V_c = 0$, which is satisfied by $\mathbf{V_b} = \mathbf{V_c} = -0.5 \text{ pu}$)_.

