### Given / conversions (all on 100 MVA base)

- Slack / bus-1: $$V1=1.05∠0∘V_1 = 1.05\angle 0^\circ$$
- Bus-3 (PV): $$∣V3∣=1.04|V_3|=1.04pu, PG3=200 MW=2.00 pu$$
- Bus-2 (PQ):  
$$P_L=400\ \text{MW}=4.00\ \text{pu},\; Q_L=250\ \text{MVar}=2.50\ \text{pu}$$ So specified injections (generation sign) are:   $$P_2^{spec}=-4.00,\quad Q_2^{spec}=-2.50;\qquad P_3^{spec}=+2.00$$
- Line reactances (resistances neglected per problem):  
$$X_{12}=0.04,\;X_{13}=0.03,\;X_{23}=0.025.$$
- Initial voltages: 
$$V_2^0=1\angle0^\circ,\;V_3^0=1.04\angle0^\circ.$$

---

## Step 1 — Build the fast-decoupled B′B' reduced matrix (for angle update)

Using the usual approximation 
$B'_{ii}=\sum_{k\ne i}1/X_{ik},\; B'_{ij}=-1/X_{ij}:$

For the non-slack buses (2 and 3) the reduced B′B' is

$$B'=\begin{bmatrix} 65 & -40\\[4pt] -40 & 73.333333 \end{bmatrix}$$

values in pu, coming from $1/X_{12}=25,\;1/X_{13}=33.3333,\;1/X_{23}=40$

Solve $B'\,\Delta\theta = \Delta P$ where $\Delta P = P^{spec}-P^{calc}$. With all initial angles zero and purely reactive network,$P^{calc}\approx0$, so $\Delta P = [ -4.0,\; 2.0]^T$ (buses 2 and 3).

Solving gives angle updates (radians):

$$\Delta\theta = \begin{bmatrix}-0.06736842\\[4pt]-0.00947368\end{bmatrix}\;\text{rad}$$

which in degrees are

$\theta_2 = -3.8599^\circ,\qquad \theta_3=-0.5428^\circ$

So after the angle-update step:

$V_2 = 1.0\angle(-3.8599^\circ),\qquad V_3 = 1.04\angle(-0.5428^\circ).$

---

## Step 2 — Q–V update (first iteration)

Only PQ buses are included in the Q–V solve. Here bus-2 is the only PQ bus (bus-3 is PV with $|V_3|$ fixed). Form the Q mismatch using the updated angles and initial magnitudes, compute $Q^{spec}-Q^{calc}$, then solve the approximate scalar FDLF equation for bus-2:

$$B''_{22}\,\Delta V_2 = \frac{\Delta Q_2}{|V_2|},$$

with $B''_{22}=65$ (same diagonal term as above).

Using the updated angles to evaluate QcalcQ^{calc} (via $S_i = V_i\overline{\sum_j Y_{ij}V_j})$, the computed network injection at bus-2 is

$$Q_{2}^{calc} \approx +2.7207567\ \text{pu}.$$

Therefore

$$\Delta Q_2 = Q_{2}^{spec}-Q_{2}^{calc} = -2.50 - 2.7207567 = -5.2207567\ \text{pu}.
$$
Thus

$$\Delta V_2 = \frac{\Delta Q_2}{B''_{22}\,|V_2|} = \frac{-5.2207567}{65\cdot 1.0} = -0.0803193\ \text{pu}.$$

Update magnitude:

$$|V_2|^{(1)} = 1.0000 + (-0.0803193) = 0.9196807\ \text{pu}.$$

---

## Final **first-iteration** phasors (rounded)

**Bus-2 (first iteration):**

- Polar: $V_2^{(1)} = 0.9196807\angle(-3.8599^\circ)\ \text{pu}$    
- Rectangular: $V_2^{(1)} \approx 0.91759 - j\,0.06191\ \text{pu}$

**Bus-3 (after angle update; voltage magnitude fixed):**

- Polar: $V_3^{(1)} = 1.040000\angle(-0.5428^\circ)\ \text{pu}$    
- Rectangular: $V_3^{(1)} \approx 1.0399533 - j\,0.0098525\ \text{pu}$

(For reference the slack bus stayed $V_1=1.05\angle0^\circ$.)
