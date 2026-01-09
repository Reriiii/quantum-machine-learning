# Lecture 1.1 - Vector Spaces, Tensor Products, and Qubits

> **Source:** [YouTube Lecture](https://www.youtube.com/watch?v=xgA4Dx_7q34&list=PLOFEBzvs-VvqJwybFxkTiDzhf5E11p8BI)

# 1. From Bits to Qubits

- Classical states for computation are either "0" or "1".
- In quantum mechanics, a state can be in *superposition*, i.e., simultaneously be in "0" and "1".
- Superpositions allow performing calculations on many states at the same time.

> $\implies$ Quantum algorithms provide exponential speed-up.

**BUT:** Once we measure the superposition state, it **collapses** into one of its states.

It is not THAT easy to design quantum algorithms, but we use **interference effects**.

## 1.1. Dirac notation & density matrices

- Used to describe quantum states. Let $a, b \in \mathbb{C}^2$.
    - **Ket:** $|a \rangle= \begin{pmatrix} a_0 \\ a_1 \end{pmatrix}$.
    - **Bra:** $\langle b| = |b \rangle ^ \dagger = \begin{pmatrix} b_0 \\ b_1 \end{pmatrix}^\dagger = \begin{pmatrix} b_0^* & b_1^* \end{pmatrix}$.
    - **Bra-Ket (Inner Product):** $\langle b|a \rangle = a_0b_0^* + a_1b_1^* = \langle a|b \rangle^* \in \mathbb{C}$.
    - **Ket-Bra (Outer Product):**
      $$|a\rangle\langle b| = \begin{pmatrix} a_0b_0^* & a_0b_1^* \\ a_1b_0^* & a_1b_1^* \end{pmatrix}$$

- We define the pure state $|0 \rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ and $|1 \rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$, which are orthogonal ($\langle 0 | 1 \rangle = 1\cdot0 + 0\cdot1=0$).

  $$|0 \rangle \langle 0 | = \begin{pmatrix} 1 \\ 0 \end{pmatrix} \begin{pmatrix} 1 & 0 \end{pmatrix} = \begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix}$$

  $$|1 \rangle \langle 1 | = \begin{pmatrix} 0 \\ 1 \end{pmatrix} \begin{pmatrix} 0 & 1 \end{pmatrix} = \begin{pmatrix} 0 & 0 \\ 0 & 1 \end{pmatrix}$$

  $$\implies \rho = \begin{pmatrix} \rho_{00} & \rho_{01} \\ \rho_{10} & \rho_{11} \end{pmatrix} = \rho_{00} |0 \rangle \langle 0| + \rho_{01} |0 \rangle \langle1| + \rho_{10} |1 \rangle \langle 0| + \rho_{11} |1 \rangle \langle1|$$

- All quantum states can be described by **density matrices**, i.e., normalized positive Hermitian operators $\rho$:
  $$tr(\rho)=1, \quad \rho \ge 0, \quad \rho=\rho^\dagger$$

  *Properties:*
  * $tr(\rho)=\rho_{00} + \rho_{11} = 1$
  * $\langle \psi | \rho | \psi\rangle \ge 0 \ \forall \ \psi$ (all eigenvalues $\ge 0$)
  * $\rho^\dagger = \begin{pmatrix} \rho_{00}^* & \rho_{10}^* \\ \rho_{01}^* & \rho_{11}^* \end{pmatrix} = \rho$

- All quantum states are normalized, i.e., $\langle\psi|\psi\rangle=1$.
  Example: $|\psi\rangle=\frac{1}{\sqrt{2}}(|0\rangle + |1\rangle) = \begin{pmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{pmatrix}$.

- **Spectral Decomposition**: For every density matrix $\rho$ exists an orthonormal basis $\{|i\rangle\}$, such that:
  $$\rho=\sum_{i}\lambda_i|i\rangle\langle i|$$
  Where:
    - $|i\rangle$: eigenstates.
    - $\lambda_i$: eigenvalues.
    - $\sum_{i}\lambda_i=1$.

- A density matrix is **pure** if $\rho=|\psi\rangle\langle\psi |$, otherwise it is called **mixed**.
    - If $\rho$ is pure: one eigenvalue is 1, all others are 0 $\implies tr(\rho^2)=\sum_{i}\lambda_{i}^2=1$.
    - If $\rho$ is mixed: $tr(\rho^2) < 1$.

**Examples:**
1.  $\rho=\begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix} = |0\rangle\langle0| \implies$ **pure**.
2.  $\rho=\begin{pmatrix} 0 & 0 \\ 0 & 1 \end{pmatrix} = |1\rangle\langle1| \implies$ **pure**.
3.  $\rho=\frac{1}{2}\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}=\frac{1}{2}(|0\rangle\langle0| + |1\rangle\langle1|) \implies tr(\rho^2)= \left(\frac{1}{2}\right)^2+\left(\frac{1}{2}\right)^2 = 0.5 < 1 \implies$ **mixed**.
4.  $\rho=\frac{1}{2}\begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}$.
    We can rewrite as:
    $$\rho = \underbrace{\left[ \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle) \right]}_{|\psi\rangle} \underbrace{\left[ \frac{1}{\sqrt{2}}(\langle 0| - \langle 1|) \right]}_{\langle\psi|} = |\psi\rangle\langle\psi|$$
    $\implies$ **pure**.

## 1.2. Measurements

- We choose orthogonal bases to describe/measure quantum states.
- During a measurement onto the basis $\{|0\rangle, |1\rangle\}$, the state will *collapse* into either state $|0\rangle$ or $|1\rangle$. As these are the two eigenstates of $\sigma_z=\begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$, we call this a **Z-measurement**.
- Other common bases:
    - **X-basis:** $\{|+\rangle \coloneqq \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle), \quad |-\rangle \coloneqq \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)\}$ (eigenstates of $\sigma_x$).
    - **Y-basis:** $\{|+i\rangle \coloneqq \frac{1}{\sqrt{2}}(|0\rangle + i|1\rangle), \quad |-i\rangle \coloneqq \frac{1}{\sqrt{2}}(|0\rangle - i|1\rangle)\}$ (eigenstates of $\sigma_y$).

**Born rule**: The probability that a state $\psi$ collapses during a projective measurement onto the basis $\{|x\rangle, |x_\perp\rangle\}$ to the state $|x\rangle$ is given by:
$$P(x)=|\langle x|\psi\rangle|^2, \quad \sum_{i}P(x_i)=1$$

**Examples:**

1.  $|\psi\rangle=\frac{1}{\sqrt{3}}(|0\rangle + \sqrt{2}|1\rangle)$ measured in the basis $\{|0\rangle, |1\rangle\}$:

    $$P(0)=\left|\left\langle 0 \middle| \frac{1}{\sqrt{3}}\left(|0\rangle + \sqrt{2}|1\rangle\right) \right\rangle \right|^2 = \left| \frac{1}{\sqrt{3}}\underbrace{\langle 0 | 0 \rangle}_{1} + \sqrt{\frac{2}{3}} \underbrace{\langle 0 | 1\rangle}_{0} \right|^2 = \frac{1}{3}$$
    $$\implies P(1) = 1 - P(0) = \frac{2}{3}$$

2.  $|\psi\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)$ measured in the basis $\{|+\rangle, |-\rangle\}$:

    $$P(+) = |\langle + | \psi \rangle|^2 = \left| \left( \frac{\langle 0| + \langle 1|}{\sqrt{2}} \right) \left( \frac{|0\rangle - |1\rangle}{\sqrt{2}} \right) \right|^2$$
    $$= \left| \frac{1}{2} (\underbrace{\langle0|0\rangle}_{1} - \underbrace{\langle0|1\rangle}_{0} + \underbrace{\langle1|0\rangle}_{0} - \underbrace{\langle1|1\rangle}_{1}) \right|^2 = |0|^2 = 0$$

    Expected result, as $\langle + | \psi \rangle = \langle + | - \rangle = 0$. Thus, $P(-) = 1$.

## 1.3. Bloch Sphere

<figure>
  <img src="./img/Bloch_Sphere.png" alt="Bloch Sphere" width="300">
  <figcaption align="center">Fig 1. Bloch Sphere Representation</figcaption>
</figure>

- We can write any normalized pure state as:
  $$|\psi\rangle = \cos\frac{\theta}{2}|0\rangle + e^{i\varphi}\sin\frac{\theta}{2}|1\rangle$$
  Where:
  - $\varphi \in [0, 2\pi)$ describes the relative phase.
  - $\theta \in [0, \pi]$ determines the probability to measure $|0\rangle$ or $|1\rangle$:
    - $P(0) = \cos^2\frac{\theta}{2}$
    - $P(1) = \sin^2\frac{\theta}{2}$

- All normalized pure states can be illustrated on the surface of a sphere with radius $|\vec{r}|=1$, called the **Bloch Sphere**.
- The coordinates are given by the **Bloch vector**:
  $$\vec{r}=\begin{pmatrix} \sin\theta \cos\varphi \\ \sin\theta \sin\varphi \\ \cos\theta \end{pmatrix}$$

**Examples:**

* $|0\rangle: \theta=0 \implies \vec{r}=(0, 0, 1)^T$ (North Pole)
* $|1\rangle: \theta=\pi \implies \vec{r}=(0, 0, -1)^T$ (South Pole)
* $|+\rangle: \theta=\frac{\pi}{2}, \varphi=0 \implies \vec{r}=(1, 0, 0)^T$
* $|-\rangle: \theta=\frac{\pi}{2}, \varphi=\pi \implies \vec{r}=(-1, 0, 0)^T$
* $|+i\rangle: \theta=\frac{\pi}{2}, \varphi=\frac{\pi}{2} \implies \vec{r}=(0, 1, 0)^T$
* $|-i\rangle: \theta=\frac{\pi}{2}, \varphi=\frac{3\pi}{2} \implies \vec{r}=(0, -1, 0)^T$

> [!WARNING]
> **BE CAREFUL:**
> * On the Bloch Sphere, angles are *twice* as large as they are in Hilbert space.
> * Example: $|0\rangle$ and $|1\rangle$ are orthogonal in Hilbert space ($90^\circ$), but on the Bloch sphere, they are opposite ($180^\circ$).
> * $\theta$ is the angle on the Bloch sphere, while $\frac{\theta}{2}$ is the parameter in the state vector.

## 2. Quantum Circuits

- **Circuit model**: Sequence of building blocks that carry out elementary computations called *gates*.

### 2.1. Single qubit gates

- Classical example: NOT gate

<figure>
  <img src="./img/Not-gate.svg" alt="Classical NOT gate" width="300">
  <figcaption align="center">Fig 2. Classical NOT gate</figcaption>
</figure>

- Quantum examples: As quantum theory is *unitary*, quantum gates are represented by *unitary matrices*: $U^\dagger U=I$.
  - $\sigma_X = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix} = |0\rangle\langle1| + |1\rangle\langle0|$ \
    $\implies \sigma_X|0\rangle = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}\begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} 0 \\ 1 \end{pmatrix} = |1\rangle$ \
    $\implies \sigma_X|1\rangle = (|0\rangle\langle1| + |1\rangle\langle0|).|1\rangle = |0\rangle \underbrace{\langle1|1\rangle}_{1} + |1\rangle \underbrace{\langle0|1\rangle}_{0}=|0\rangle$

      $\implies$ **Bit Flip** $\hat{=}$ NOT-gate
  
  - $\sigma_Z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix} = |0\rangle\langle0| - |1\rangle\langle1|$ \
    $\implies \sigma_Y|+\rangle = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix} \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ -1 \end{pmatrix} = |-\rangle$ \
    $\implies \sigma_Y|+\rangle =|-\rangle$\
    $\implies$ **Phase Flip**: Rotation around Z-axis by $\pi$.

  - $\sigma_Y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix} = i\sigma_X\sigma_Z \implies$ **Bit & Phase Flip**.
  - $\sigma_X, \sigma_Y, \sigma_Z$ are the so-called *Pauli matrices* and $\sigma_i^2 = I = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$.
  - Together with identity $I$ they form a basis of 2x2 matrices.
  
- **Hadamard Gate**: One of the most important gates for quantum circuits.
  
  $H= \frac{1}{\sqrt{2}} \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix} = \frac{1}{\sqrt{2}} \left( |0\rangle\langle0| + |0\rangle\langle1| + |1\rangle\langle0| - |1\rangle\langle1| \right)$

  $\implies H|0\rangle = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix} \begin{pmatrix} 1 \\ 0 \end{pmatrix} = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = |+\rangle$

  $\implies H|1\rangle = \frac{1}{\sqrt{2}} \left( |0\rangle\langle0| + |0\rangle\langle1| + |1\rangle\langle0| - |1\rangle\langle1| \right)|1\rangle = \frac{1}{\sqrt{2}} (|0\rangle - |1\rangle) = |-\rangle$

  $\implies$ Creates superposition! Also $H|+\rangle=|0\rangle, \ H|-\rangle=|1\rangle$

  Use to change between X and Z basis.

- Similarly, as $S=\begin{pmatrix} 1 & 0 \\ 0 & i \end{pmatrix}$ adds $90^\circ$ to the phase $\varphi$:
  - $S|+\rangle = |+i\rangle$
  - $S|-\rangle = |-i\rangle$
  - $SH$ is applied to change from $Z$ to $Y$ basis.

### 2.2. Multipart Quantum States

- We use *tensor products* to describe miltiple states:
  
  $|a\rangle \otimes |b\rangle = \begin{pmatrix} a_1 \\ a_2 \end{pmatrix} \otimes \begin{pmatrix} b_1 \\ b_2 \end{pmatrix} = \begin{pmatrix} a_1b_1 \\ a_1b_2 \\ a_2b_1 \\ a_2b_2 \end{pmatrix}$ 

  Example: System A is in state $|1\rangle_A$ and system B is in statee $|0\rangle_B$\
  $\implies$ The total (bipartile) state is $|10\rangle_{AB}:=|1\rangle_A \otimes |0\rangle_B = \begin{pmatrix} 0 \\ 1 \end{pmatrix} \otimes \begin{pmatrix} 1 \\ 0 \end{pmatrix} =  \begin{pmatrix} 0 \\ 0 \\ 1 \\ 0 \end{pmatrix}$
  
- Remark: States of this form are called **uncorrelated**, but there are also bipartile states that cannot be written as $|\psi\rangle_A \otimes |\varphi\rangle_B$. These states are *correlated* and sometimes even *entangled*. \
e.g. $|\Phi^+\rangle = \frac{1}{\sqrt{2}} (|00\rangle_{AB} + |11\rangle_{AB}) = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ 0 \\ 0 \\ 1 \end{pmatrix}$

### 2.3. Two-qubit Gates