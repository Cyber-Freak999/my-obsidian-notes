When a **voltage source** is applied to a load consisting of a **resistor in parallel with an inductive reactance**, you can solve for the instantaneous power absorbed by each component, and the real power, reactive power, and power factor absorbed by the total load by following a series of steps based on the principles of AC circuits.

First, let's establish some basic definitions for sinusoidal AC circuits:

- The **instantaneous voltage** is typically represented as $v(t) = V_M \cos(\omega t + \theta_V)$, where $V_M$ is the maximum voltage and $\theta_V$ is its phase angle.
- The **instantaneous current** is represented as $i(t) = I_M \cos(\omega t + \theta_I)$, where $I_M$ is the maximum current and $\theta_I$ is its phase angle.
- The **instantaneous power** $p(t)$ delivered to the load at any moment is the product of the instantaneous voltage and current: $p(t) = v(t)i(t)$.
- The **rms (root mean square) value** of voltage $|V|$ is $V_M / \sqrt{2}$, and for current $|I|$ is $I_M / \sqrt{2}$. These are the values typically read by meters.
- The **phase angle** $\theta$ is the difference between the voltage and current phase angles, $\theta = \theta_V - \theta_I$. For an **inductive load**, the current lags the voltage, so $\theta$ is positive.

---

### Instantaneous Power Absorbed by the Resistor and the Inductor

To find the instantaneous power absorbed by each parallel component, you first need to determine the instantaneous current flowing through each. Since the resistor ($R$) and inductive reactance ($X_L$) are in parallel, they both experience the same instantaneous voltage from the source.

Let the instantaneous source voltage be $v(t) = V_M \cos(\omega t + \theta_V)$.

1. **Instantaneous Power Absorbed by the Resistor:**
    
    - The **current through the resistor** $i_R(t)$ will be in phase with the voltage across it. So, $i_R(t) = \frac{V_M}{R} \cos(\omega t + \theta_V)$.
    - The **instantaneous power absorbed by the resistor** $p_R(t)$ is the product of the instantaneous voltage across it and the current through it: $p_R(t) = v(t)i_R(t) = \left[V_M \cos(\omega t + \theta_V)\right] \left[\frac{V_M}{R} \cos(\omega t + \theta_V)\right]$.
    - Using the trigonometric identity $\cos^2 A = \frac{1}{2}(1 + \cos 2A)$, this simplifies to $p_R(t) = \frac{V_M^2}{2R} \left[1 + \cos(2(\omega t + \theta_V))\right]$. This power is always positive or zero, indicating that energy is continuously absorbed by the resistor and converted to another form (e.g., thermal energy).
2. **Instantaneous Power Absorbed by the Inductor:**
    
    - The **current through the inductor** $i_L(t)$ will lag the voltage across it by 90 degrees. So, $i_L(t) = \frac{V_M}{X_L} \cos(\omega t + \theta_V - 90^\circ)$.
    - The **instantaneous power absorbed by the inductor** $p_L(t)$ is the product of the instantaneous voltage across it and the current through it: $p_L(t) = v(t)i_L(t) = \left[V_M \cos(\omega t + \theta_V)\right] \left[\frac{V_M}{X_L} \cos(\omega t + \theta_V - 90^\circ)\right]$.
    - Using the identity $\cos A \cos(A-90^\circ) = \cos A \sin A = \frac{1}{2}\sin 2A$, this simplifies to $p_L(t) = \frac{V_M^2}{2X_L} \sin(2(\omega t + \theta_V))$.
    - This instantaneous power term is alternately positive and negative, pulsating at twice the source frequency, and has an average value of zero. When $p_L(t)$ is positive, energy is stored in the magnetic field of the inductor, and when negative, energy is returned from the magnetic field to the source.

---

### Real and Reactive Power Absorbed by the Load and the Power Factor

To find the **real power**, **reactive power**, and **power factor** for the total load, it's often easiest to work with **phasors** and **complex power**.

Let the rms source voltage be $V = |V| \angle \theta_V$.

1. **Calculate Currents through each parallel branch:**
    
    - **Current through resistor:** $I_R = \frac{V}{R} = \frac{|V|}{R} \angle \theta_V$.
    - **Current through inductor:** The impedance of the inductor is $Z_L = jX_L = X_L \angle 90^\circ$. So, $I_L = \frac{V}{jX_L} = \frac{|V|}{X_L} \angle (\theta_V - 90^\circ)$.
2. **Calculate Total Current from the Source:**
    
    - The total current is the phasor sum of the individual branch currents: $I_{total} = I_R + I_L$.
    - Let $I_{total} = |I_{total}| \angle \theta_I$.
3. **Real Power (P) Absorbed by the Load:**
    
    - **Real power** is the average power developed by the load. It is the power absorbed by the resistive component of the load.
    - The formula for real power is $P = |V||I_{total}|\cos\theta$, where $\theta = \theta_V - \theta_I$ is the phase angle between the total voltage and total current.
    - Since only the resistor absorbs real power in an ideal parallel R-L circuit, you can also calculate it as $P = \frac{|V|^2}{R}$ or $P = |I_R|^2 R$.
    - Real power is measured in **watts (W)**, kilowatts (kW), or megawatts (MW).
4. **Reactive Power (Q) Absorbed by the Load:**
    
    - **Reactive power** accounts for the energy oscillating into and out of the reactive elements (inductors or capacitors) of the load.
    - The formula for reactive power is $Q = |V||I_{total}|\sin\theta$.
    - For a purely inductive load, Q is positive.
    - Since only the inductor absorbs reactive power in an ideal parallel R-L circuit, you can also calculate it as $Q = \frac{|V|^2}{X_L}$ or $Q = |I_L|^2 X_L$.
    - Reactive power is measured in **volt-ampere reactive (var)**, kilovars (kvar), or megavars (Mvar).
5. **Power Factor (PF):**
    
    - The **power factor** is defined as the cosine of the phase angle $\theta$ between the voltage and the current.
    - It can be calculated as $\text{PF} = \cos\theta = \frac{P}{|S|}$, where $|S|$ is the **apparent power**.
    - The **apparent power** $|S|$ is the product of the rms voltage and rms total current, $|S| = |V||I_{total}|$, and is measured in **volt-ampere (VA)**, kilovolt-ampere (kVA), or megavolt-ampere (MVA). It is also the magnitude of the complex power $S = P + jQ$, so $|S| = \sqrt{P^2 + Q^2}$.
    - Since the load consists of a resistor in parallel with an inductive reactance, it is an **inductive circuit**, and thus the **power factor will be lagging**. This means the total current lags the applied voltage.

**Summary of Calculation using Complex Power:**

A more concise way to determine real and reactive power for the entire load is by calculating the **complex power** $S$:

- Calculate the admittance of each parallel component:
    - $Y_R = \frac{1}{R}$
    - $Y_L = \frac{1}{jX_L} = -j\frac{1}{X_L}$
- The **total admittance** of the load is $Y_{total} = Y_R + Y_L = \frac{1}{R} - j\frac{1}{X_L}$.
- The **complex power** $S$ is given by $S = V I_{total}^* = P + jQ$.
- Alternatively, $S = |V|^2 Y_{total}^*$.
    - If $V = |V| \angle \theta_V$, then $S = |V|^2 (\frac{1}{R} + j\frac{1}{X_L}) = \frac{|V|^2}{R} + j\frac{|V|^2}{X_L}$.
- From $S = P + jQ$:
    - The **real power** $P = \frac{|V|^2}{R}$ (the real part of S).
    - The **reactive power** $Q = \frac{|V|^2}{X_L}$ (the imaginary part of S).
- The **power factor** $\text{PF} = \frac{P}{|S|}$.
    - The **apparent power** $|S| = \sqrt{P^2 + Q^2}$.
- Since $Q$ is positive for an inductive load, the power factor is **lagging**.








