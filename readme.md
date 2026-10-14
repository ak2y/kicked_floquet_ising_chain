# [Team Schrodinger's Coder] · Qiskit Fall Fest 2026 · Track [3]: [Simulating Quantum Dynamics: The Transverse-Field Ising Model]

<!--
How to use this template:
1. Copy this file into the root of your team's public GitHub repo and rename it README.md.
2. Replace everything in [square brackets] and delete these comments.
3. Keep every heading. Write "none" where something does not apply.
-->

| | |
|---|---|
| **Team** | Team Schrodinger's Coder |
| **Members** | [Akash Yadav, akash.a2y@gmail.com], [Hemin Roy, heminroy08@gmail.com,], [Shradul Sharma, shradul24538@iiitd.ac.in] |
| **Track** | 3 · Quantum Simulation |
| **Level reached** | Advanced |
| **Code files** | In [src](src)|
| **Slides** | [`slides.pdf` ](qiskit_fallfest.pdf)|

## Summary

Simulation of the Floquet-kicked Ising system and computation of Imbalance starting from the Néel state to determine whether localisation occurs. We can observe both localised and non-localised states, depending on the parameters. 

## Approach
We consider 1D spin-1/2 chain with nearest-neighbour Ising interactions, a longitudinal magnetic field, and periodic transverse kicks. The Hamiltonian is

$$
\boxed{
H(t)=J_z\sum_{i=0}^{N-2}Z_iZ_{i+1}
+h_z\sum_{i=0}^{N-1}Z_i
+h_x\sum_n\delta(t-nT)\sum_{i=0}^{N-1}X_i.
}
$$
Imbalance:- 
$$
\boxed{
\hat{\mathcal{I}} =
\frac{1}{L}
\sum_{i=0}^{L-1} (-1)^i Z_i
}
$$

We used Imbalance as an observable because the results are either +1 or -1 for the selected parameters that convert the circuit to a Clifford circuit. Once we get results from the hardware and Clifford data, we know the upper bound of the error from the hardware. Used ZNE as Error mitigation method.


## Results
Imbalance from N=100 Floquet-kicked Ising system with clifford parameters(Jz•T = hz•T = hx = π/2):
![!\[alt text\](image.png)](images/image.png)

Maximum 2Q depth = 200

| Floquet Step | Quantity | Your Result (IBM Marakesh) | Reference (Clifford) | Absolute Difference |
|---:|---|---:|---:|---:|
| 5  | Imbalance | -1.139428 | -1.000000 | 0.139428 |
| 10 | Imbalance | 1.191102  | 1.000000  | 0.191102 |
| 15 | Imbalance | -1.139535 | -1.000000 | 0.139535 |
| 20 | Imbalance | 1.130892  | 1.000000  | 0.130892 |
| 25 | Imbalance | -1.148508 | -1.000000 | 0.148508 |
| 30 | Imbalance | 1.094031  | 1.000000  | 0.094031 |
| 35 | Imbalance | -1.032225 | -1.000000 | 0.032225 |
| 40 | Imbalance | 0.981044  | 1.000000  | 0.018956 |
| 45 | Imbalance | -0.877113 | -1.000000 | 0.122887 |
| 50 | Imbalance | 0.805764  | 1.000000  | 0.194236 |

## How we checked our results
We matched our results to the Clifford Circuit, and in the future we can use classical methods such as Pauli propagation and the tensor network method.

## Hardware runs

| Backend | Job | Job ID | PUBs | QPU Time |
|---|---|---|---:|---|
| ibm_marrakesh | Job 1 | db7r0u0r1c5c738l4kd0 | 11 | — |
| ibm_marrakesh | Job 2 | db7r0v2raffc73fb47sg | 10 | — |
| ibm_marrakesh | Job 3 | db7r0vur6oqs73885550 | 10 | — |
| ibm_marrakesh | Job 4 | db7r10qraffc73fb4810 | 10 | — |
| ibm_marrakesh | Job 5 | db7r11qraffc73fb4830 | 10 | — |
| **Total** | **5 jobs** | — | **51** | **8m 53s (533 seconds)** |

## Limitations
ZNE can yield worse results as circuit size increases, and with higher noise factors, more gates are used; we can use other methods like ODR, which doesn't increase circuit depth. And QPU time is very high, so we can't run non-Clifford circuits on hardware, and we didn't benchmark against classical methods.

## How to run

- Python version: [3.12]
- Install: `pip install -r requirements.txt` (or list the packages and versions)
- Run: for hardware run use [job_submisson.ipynb](src/job_submisson.ipynb) and for AerSimulator use [kicked_floquet_ising.ipynb](src/kicked_floquet_ising.ipynb)

## Credits

- Track tutorial: adapted from the BasQ Qiskit Fall Fest 2026 tutorials by Benjamin Tirado (text CC BY 4.0, code Apache 2.0).
- AI tools used: ChatGPT for data plotting, text formatting and grammar correction.
