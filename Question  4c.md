# A two pole synchronous generator has a rating  of 250MVA 60Hz with an inertia constant H of 5.4 MJ/MVA. Assume the machine runs steadily at synchronous speed with a shaft input of 331.10hp. The electrical power developed suddenly changed from its normal value to a value of 200 MW. Determine the:
- Kinectic energy stored by the synchronous generator
- Acceleration or deceleration of the rotor
- Change in the power angle if the acceleration computed for the generator computed for the generator is constant for a period of 9 cycles and the rpm at the end of 9 cycles
  
This problem analyzes the dynamic behavior of a synchronous generator following a disturbance, utilizing the machine's inertia constant ($H$) and the swing equation. Since the machine is running steadily at synchronous speed before the change, the initial electrical power developed is equal to the mechanical shaft input power ($P_{e, initial} = P_{m, initial}$).

We rely on the parameters and methodology presented in an equivalent problem description within the sources (Problem 11.3). We assume the intended mechanical input is $\mathbf{331,100 \text{ hp}}$, as used in the source calculation corresponding to these generator parameters.

### Given Parameters:

*   Generator Rating ($S_B$): $250 \text{ MVA}$
*   Inertia Constant ($H$): $5.4 \text{ MJ/MVA}$
*   Frequency ($f$): $60 \text{ Hz}$
*   Number of poles ($P$): 2
*   Shaft Input ($P_m$): $331,100 \text{ hp}$ (Equivalent to $247 \text{ MW}$ or $0.988 \text{ pu}$).
*   New Electrical Power Output ($P_e$): $200 \text{ MW}$ (Equivalent to $0.8 \text{ pu}$).
*   Time Period ($\Delta t$): 9 cycles.

---

### 1. Kinetic Energy Stored by the Synchronous Generator ($W_k$)

The kinetic energy stored in the rotor masses at synchronous speed ($W_k$) is found using the inertia constant ($H$) and the machine rating ($S_{mach}$):

$$\mathbf{W_k} = H \times S_{mach}$$
$$W_k = 5.4 \text{ MJ/MVA} \times 250 \text{ MVA} = \mathbf{1350 \text{ MJ}}$$

### 2. Acceleration or Deceleration of the Rotor

We first determine the accelerating power ($P_a$) in per unit (pu), where the accelerating power is the difference between the mechanical input power ($P_m$) and the electrical output power ($P_e$):

$$P_{m, pu} = \frac{331,100 \text{ hp} \times 746 \times 10^{-6} \text{ MW/hp}}{250 \text{ MVA}} = \frac{247 \text{ MW}}{250 \text{ MVA}} = 0.988 \text{ pu}$$.
$$P_{e, pu} = \frac{200 \text{ MW}}{250 \text{ MVA}} = 0.8 \text{ pu}$$.

**Accelerating Power ($P_a$):**
$$P_a = P_{m, pu} - P_{e, pu} = 0.988 - 0.8 = \mathbf{0.188 \text{ pu}}$$

Since $P_a$ is positive, the rotor is **accelerating**.

The acceleration ($\frac{d^2\delta}{dt^2}$) is calculated using the swing equation, where $\delta$ is in electrical degrees [257, Eq. 16.14]:

$$\frac{d^2\delta}{dt^2} = \frac{180 f}{H} P_a$$
$$\frac{d^2\delta}{dt^2} = \frac{180 \times 60 \text{ Hz}}{5.4} \times 0.188 \text{ pu}$$
$$\frac{d^2\delta}{dt^2} = \mathbf{376 \text{ degrees/sec}^2}$$.

To express the acceleration in revolutions per minute per second (rpm/s), we convert the angular acceleration:
$$\text{Acceleration (rpm/s)} = \frac{60}{360} \times 376 \text{ degrees/sec}^2 \approx \mathbf{62.6667 \text{ rpm/sec}}$$.

---

### 3. Change in Power Angle and RPM at the end of 9 Cycles

The period of 9 cycles in seconds is:
$$\Delta t = \frac{9 \text{ cycles}}{60 \text{ Hz}} = 0.15 \text{ seconds}$$

#### Change in Power Angle ($\Delta \delta$)

Assuming the acceleration is constant for this short period, the change in the power angle ($\Delta \delta$) is calculated using the kinematic formula for displacement ($\Delta \delta = \frac{1}{2} a t^2$), where the initial velocity is zero relative to the synchronous reference frame:

$$\Delta \delta = \frac{1}{2} \left(\frac{d^2\delta}{dt^2}\right) (\Delta t)^2$$
$$\Delta \delta = \frac{1}{2} (376 \text{ deg/sec}^2) (0.15 \text{ s})^2$$
$$\Delta \delta = \frac{1}{2} (376) (0.0225) = \mathbf{4.23 \text{ electrical degrees}}$$.

#### RPM at the end of 9 cycles

First, determine the synchronous speed ($n_s$) for a 2-pole, 60 Hz generator:
$$n_s = \frac{120 f}{P} = \frac{120 \times 60}{2} = 3600 \text{ rpm}$$.

The speed ($n$) at the end of the 0.15-second period is the synchronous speed plus the total increase in speed ($\Delta n$):

$$n = n_s + (\text{Acceleration in rpm/s}) \times \Delta t$$
$$n = 3600 \text{ rpm} + (62.6667 \text{ rpm/s}) \times 0.15 \text{ s}$$
$$n = 3600 + 9.40 \approx \mathbf{3609.4 \text{ rpm}}$$