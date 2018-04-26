---
title: Quantum Computing - Report 
category: Physics
excerpt: |    
  Quantum Computing - Report
feature_image: "https://unsplash.it/1300/400?random"
---

Quantum Computing and its Physical Realization

<!-- more -->

# Abstract

Quantum computing has recently been a heated topic: The decreasing dimension of classical computing circuits makes it inevitable that quantum effects will take effect. On the other hand, many featured properties of quantum computing has made it a potential candidate for the next generation of computing device, if the growth of computing power is expected to keep in accordance with Moore’s Law. In specific, some quantum algorithms have shown exponential speedup compared with classical algorithms. 

In this report, first I will review the formalism of quantum computing, and provide some mathematical proof to theorems or give some concrete examples. Then one of the most famous algorithms – quantum Fourier transform(QFT) and its application will be discussed. Finally, an experimental confirmation using QFT and machine learning techniques to classify digits will be analyzed, and some discussions will be proposed. 

# Formalism

First I will introduce the elements of quantum computation. Similar to  classical computation, quantum computation may be decomposed into three parts: qubit, which is the “memory” and computational unit of quantum computing; quantum gate, which implements unitary transformation on quantum states; measurement, during which the desired information is extracted. The formalism of the three parts will be discussed below. As for the implementation of quantum computing algorithms, it generally involves three steps: encoding the input state, conducting unitary transformation on the previous state and measuring the output state. An example of this will be postponed until later.

### Qubits

Analogous to a classical bit in classical computers, a qubit is the basic two-level computational unit governed by quantum mechanics. It is represented as 

$$
| \psi \rangle = \alpha | 0 \rangle + \beta | 1 \rangle 
$$

It can be seen that rather than only take values $$0$$ and $$1$$ as in classical computers, the coefficients $$\alpha$$ and $$\beta$$ take continuous values. Unfortunately, measurement theory tells us that only one bit of information may be acquired when the state is measured, thus only state $$\mid 0 \rangle$$ or state $$\mid 1 \rangle$$ may be detected in experiments, and the coefficients cannot be acquired directly.  

More generally, an n-qubit state may be represented as  

$$
\begin{split}
| \psi \rangle = \sum^{2^n-1}_{i=0} c_i | i \rangle 
\end{split}
$$

constrained by the normalization condition  

$$
 \sum^{2^n-1}_{i=0} |c_i|^2 =1. 
$$  


It is worth mentioning that with $$n$$ qubits, the formed computational basis has $$2^n$$ states, and thus the potential storage capabilities have exponential increase over classical algorithms. However, the output of the measurement process is constrained to one explicit state from the Hilbert space, and in a quantum algorithm, the whole process must be repeated several times to obtain desired degree of accuracy of the solution.  

### Quantum Gates
Quantum gates represent the unitary transformation between quantum states, where the 'unitary' property comes from the fact that the norm of the states must be preserved. In the single-qubit case, gates are described by $$2 \times 2$$ unitary matrices.  

##### Hadamard Gate and Phase Gate
One of the most important matrices is the Hadamard gate(denoted as $$H$$), and its matrix form for single qubit is 
          

$$
H= \frac{1}{\sqrt{2}}\begin{bmatrix}
                    1 & 1\\ 
                    1 & -1 
                    \end{bmatrix}
$$

It can be generalized to arbitrary $$n$$-qubit case by iteration. What's more, one useful property of the general Hadamard gate is that the superposition of all states in the computational basis can be constructed by applying Hadamard gate on the state $$|000.. \rangle$$ with $$n$$ qubits:

$$
\begin{equation}
H_n\Ket{\psi_n}= \frac{1}{\sqrt{2}}\begin{bmatrix}  %需要修改！
                     H_{n-1} & H_{n-1}\\
                     H_{n-1} & -H_{n-1}
                    \end{bmatrix}
\begin{bmatrix}
                     1 \\
                     \mathbf{0_{2^n-1}} 
                    \end{bmatrix}
                    =\begin{bmatrix}
                     1 \\
                     \vdots\\   %点点点模板
                     1 
                    \end{bmatrix}
\end{equation}
$$


which will be useful in many algorithms. Here the operator $H_n$ operates on n qubits, and thus has dimension $2^n \times 2^n$.

\bigskip

\noindent Another important single qubit gate is the phase gate ($S$):
\begin{equation}
S= \begin{bmatrix}
   1 & 0\\
   0 & i
    \end{bmatrix},
\end{equation}
and it is apparent that the phase gate $S$ transforms a generic state $\Ket{\psi} = a \Ket{0} + b\Ket{1}$ into the state $\Ket{\psi} = a \Ket{0} + i ~b\Ket{1}$. Under the Bloch sphere representation of qubits, the effect of the phase gate may be visualized as the rotation of the state vector by an angle $\pi/2$ along the $z$ axis.
\subsubsection{Arbitrary Gate}
Next we discuss the generalization of the phase operator into rotation operators about the three axes: we take rotation about x-axis as an example,
\begin{gather}   
R_x(\theta)=e^{-i\theta X/2} = ~ 
%\begin{bmatrix}
%                              \cos \frac{\theta}{2} & - i \sin \frac{\theta}{2}\\
%                          - i \sin \frac{\theta}{2} &      \cos \frac{\theta}{2}
%    \end{bmatrix}, \\
%R_y(\theta)=e^{-i\theta Y/2} = ~ \begin{bmatrix}
%   \cos \frac{\theta}{2} & -  \sin \frac{\theta}{2}\\
%   \sin \frac{\theta}{2} & \cos \frac{\theta}{2}
%    \end{bmatrix}, \\ 
R_z(\theta)=e^{-i\theta Z/2} = ~ \begin{bmatrix} %单个空格模板
   e^{- i \theta /2} & 0 \\
   0 &  e^{ i \theta /2}
    \end{bmatrix},
\end{gather}
and similar for rotation operators along the other two directions. More generally, the following property which I am going to prove guarantees the completeness of single qubit gates.
\bigskip

Any unitary single-qubit gate may be represented in the form $U = e^{i\alpha} R_{\vec{n}}(\theta)$
for some real numbers $\alpha$ and $\theta$, 3-D unit vector $\vec{n}$, and the rotation operator $R_{\vec{n}}(\theta)=\cos{\frac{\theta}{2}} I − i\sin{\frac{\theta}{2}}\cdot (n_x X + n_y Y + n_z Z).$


\begin{proof}
To decompose any single qubit operator 
$U$, first we calculate the overall phase $\alpha$. Consider 
\begin{equation}
|\det U|^2 = \det U \cdot (\det U)^\dag = \det U \det U^\dag = det UU^\dag = 1  ,  
\end{equation} thus $\det U$ can be regarded a phase. We choose $e^{2 i \alpha} = \det U$, then $U = e^{i \alpha} V$, and $\det V = 1$.
Next we decompose the matrix $V$  using the given Pauli matrices:
\begin{equation}
 V= v_0 I + v_x X + v_y Y + v_z Z.
\end{equation}  %下面是小matrix模板
If we denote the matrix $V$ as $\bigl(\begin{smallmatrix}
a&b \\ c&d
\end{smallmatrix} \bigr)$,
by comparing the coefficients on both sides, we may get, $v_0 = (a+d)/2, v_x = (b+c)/2, v_y = (c-b)/2i, v_z = (a-d)/2$.

Imposing the condition that $V$ is unitary, \begin{equation}
\begin{split}
V^\dag V  = &(v_0 I + v_x X + v_y Y + v_z Z)^\dag (v_0 I + v_x X + v_y Y + v_z Z) \\
 = & |v_0|^2 + |v_x|^2 + |v_y|^2 + |v_z|^2)I + (v_0^* v_x + v_x^* v_0 + i v_y^* v_z - i v_z^* v_y )X + \\
& (v_0^* v_y + v_y^* v_0 + i v_z^* v_x - i v_x^* v_z ))Y +  (v_0^* v_z + v_z^* v_0 + i v_x^* v_y - i v_y^* v_x) Z\\
= & I.
\end{split}
\end{equation}
To satisfy the up-left element, we should have $|v_0|^2 + |v_x|^2 + |v_y|^2 + |v_z|^2=1$. Define $\cos (\theta/2)= |v_0|$, then $|v_x|^2 + |v_y|^2 + |v_z|^2=\sin^2 (\theta/2)$. The symmetric first two terms of  $X, Y$ and $Z$ and the asymmetric last two terms encourage us to reformulate them using cross product:
\begin{equation} \label{cross}
    2 Re(v_0) \cdot Re(\vec{v}) + 2 Im(v_0) \cdot Im(\vec{v}) + i ~ \vec{v^*} \times \vec{v} = \vec{0}.  
\end{equation}
\bigskip 
\bigskip
\newpage
\bigskip
Introduce the the rotation vector notation $\vec{n}$, and we have,
\begin{equation}
    (n_x,n_y,n_z) = \frac{i}{\sin(\theta /2)} (v_x,v_y, v_z).
\end{equation}

First $|n_x|^2 + |n_y|^2 + |n_z|^2 = 1$, thus the normalization condition is achieved; $v_0$ is real, $\vec{v}$ is purely imaginary, and $\vec{v^*}$ is parallel to $\vec{v}$, thus the Equation \ref{cross} is satisfied. Finally, consider the determinant of $V$:
\begin{equation}
    V = \begin{bmatrix}
      \cos{\frac{\theta}{2}} - i \sin{\frac{\theta}{2}} n_z & - i \sin{\frac{\theta}{2}} n_x - \sin{\frac{\theta}{2}} n_y \\
      - i \sin{\frac{\theta}{2}} n_x + \sin{\frac{\theta}{2}} n_y & \cos{\frac{\theta}{2}} + i \sin{\frac{\theta}{2}} n_z
    \end{bmatrix},
\end{equation}
thus $\det (V) =  \cos^2{\frac{\theta}{2}} + \sin^2{\frac{\theta}{2}} (n_x^2+n_y^2+n_z^2) = 1$, and thus the requirement that $\det(V) = 1$ is fulfilled. Thus all conditions are satisfied. 

In summary, for any unitary $2 \times 2$ matrix, we can find angle $\theta$, phase $\alpha$ and unit vector $\vec{n}$ so that the matrix can be decomposed as 
\begin{equation}
   U= e^{i\alpha}R_{\vec{n}}(\theta) = e^{i\alpha} [\cos{\frac{\theta}{2}} I − i\sin{\frac{\theta}{2}}\cdot (n_x X + n_y Y + n_z Z)].
\end{equation}
\end{proof}
%(Explain Rz; Generalize Rz to Ry and Rx; Prove H as prod of Rx and RzProve )


\subsection{Multiple Qubit Gates}
Before introducing multiple qubit states, first we claim that entanglement states cannot be generated simply with single qubit gates: assume the system starts with a separable state, $\Ket{\psi} = \Ket{\psi_{n-1}}\otimes \dots \otimes \Ket{\psi_{0}}$, and multiple single-qubit gates are implemented: $U = U_{n-1} \otimes \dots \otimes U_0 $, then the final state can still be represented as $\Ket{\psi'} = \Ket{\psi'_{n-1}}\otimes \dots \otimes \Ket{\psi'_{0}}$, and the qubits are still disentangled. Thus to fully utilize the superposition state, we need to introduce multiple-qubit operations. Here we restrict to two qubit gates, and higher dimension gates are easy to generalize. %prime和otimes模板

\bigskip
\noindent First I will introduce the swap gate, which switch the state functions of two qubits, and the operator can be represented as: 
\begin{equation} \Qcircuit @C=1em @R=2em {
& \qswap & \qw \\
& \qswap \qwx & \qw
} \end{equation}  %swap模板
and the matrix representation is 
\begin{equation} \label{swap}
SWAP = \begin{bmatrix}
                    1 & 0 & 0 & 0\\
                    0 & 0 & 1 & 0\\
                    0 & 1 & 0 & 0\\ 
                    0 & 0 & 0 & 1 
                    \end{bmatrix}.  
\end{equation}

\bigskip
\noindent 
One key two-qubit gate is the controlled-$NOT$ gate, which performs the $NOT$ operation on the second qubit conditioning on the truth of the first qubit. The representation of $CNOT$ is
\begin{equation}
\Qcircuit @C=1em @R=1.5em {
& \ctrl{1} & \qw \\
& \targ  & \qw
}
\end{equation}

\begin{equation}
   CNOT=  \begin{bmatrix}
        1 & 0 & 0 & 0 \\
        0 & 1 & 0 & 0 \\
        0 & 0 & 0 & 1 \\
        0 & 0 & 1 & 0 
    \end{bmatrix},
\end{equation}

Next I will elaborate on controlled operations by referring to a specific circuit using Controlled-phase shift operators to prepare a general superposition state, which is a core step in later parts of the report.

\subsection{An Example Circuit} \label{PRE}
Assume we want to encode the superposition of two states $\Phi_1 =\begin{bmatrix} 0.987 \\ 0.159 \end{bmatrix}$, and $\Phi_2 =\begin{bmatrix} 0.354 \\ 0.935 \end{bmatrix}$ into the state $\Ket{\beta_1} \Ket{\Phi_1} + \Ket{\beta_2} \Ket{\Phi_2}$, which is part of the preparation process in the experiment\cite{EXP}, and I will give the mathematical deduction of the circuit operations.

Consider the circuit below, where the first qubit starts from the state $\Ket{\phi} = \alpha_1 \Ket{0} + \alpha_2 \Ket{1}$, and the second qubit starts from the state $\Ket{\psi} = \beta_1 \Ket{0} + \beta_2 \Ket{1}$:
\begin{equation}
\Qcircuit @C=1em @R=1.5em {
\lstick{\ket{\phi}} & \ctrl{1}  & \ctrl{1} & \meter & \qw \\
\lstick{\ket{\psi}} & \ctrlo{1}\qw & \ctrl{1} \qw & \qw &\qw \\
\lstick{\ket{0}} & \gate{R_y ^{\,\theta_1}}     & \gate{R_y ^{\,\theta _2}}   & \qw & \qw 
}
\end{equation} %Controlled 模板
The circuit operates as follows:
\begin{equation}
\begin{split}
\Ket{\phi}\Ket{\psi}\Ket{0} & =\big [\alpha_1 \Ket{0} + \alpha_2 \Ket{1} \big] \otimes \big [\beta_1 \Ket{0} + \beta_2 \Ket{1} \big] \otimes \Ket{0} \\
& \to \alpha_1 \Ket{0\psi 0} + \alpha_2 \Ket{1} \otimes \Bigg[\beta_1 \Ket{0} \otimes \big[\cos{\frac{\theta_1}{2}}\Ket{0} + \sin{\frac{\theta_1}{2}}\Ket{1}\big] + \beta_2 \Ket{1}\big] \Bigg]\\
& \to \alpha_1 \Ket{0\psi 0} + \alpha_2 \Ket{1} \otimes \Bigg[\beta_1 \Ket{0} \otimes \big[\cos{\frac{\theta_1}{2}}\Ket{0} + \sin{\frac{\theta_1}{2}}\Ket{1}\big] + \\
 & \qquad \qquad \qquad \qquad \qquad \quad \beta_2 \Ket{1} \otimes \big[\cos{\frac{\theta_2}{2}}\Ket{0} + \sin{\frac{\theta_2}{2}} \Ket{1}\big] \Bigg] 
\end{split}
\end{equation}
Conditioning on the measurement result of the first qubit is $\Ket{1}$, and the  first rotation operator contains the rotation angle $\theta_1$ satisfies $\tan {\frac{\theta_1}{2}}= \frac{0.159}{0.987}$, and the second  $\theta_2$ satisfies  $\tan {\frac{\theta_2}{2}}= \frac{0.935}{0.354}$, then the state of the qubits reduces to
\begin{equation}
    \beta_1 \Ket{0} \begin{bmatrix}
                    \cos \frac{\theta_1}{2} \\
                    \sin \frac{\theta_1}{2}
                    \end{bmatrix} +
    \beta_2 \Ket{1} \begin{bmatrix}
                    \cos \frac{\theta_2}{2} \\
                    \sin \frac{\theta_2}{2}
                    \end{bmatrix},
\end{equation}
as desired.

\section{Quantum Algorithm}
In the past few decades, many quantum algorithms solving specific fields of questions have been proposed, and some of them achieves impressive speedup over their classical counterparts. In specific, three most prominent algorithms are quantum search, quantum Fourier transform and quantum simulation of dynamic systems. Here I will mainly focus on quantum Fourier transform algorithm, which is a crucial step in later discussions.

\subsection{Quantum Fourier Transform}

\subsubsection{Quantum Fourier Transform Formalism}
Analogous to the classical discrete Fourier transform, quantum Fourier transform samples the orthogonal basis states with varying frequencies. With an orthogonal basis $\Ket{0}, ... , \Ket{N - 1}$, the quantum Fourier transform acting on the quantum state $\Ket{j}$ outputs the state 
\begin{equation}
\Ket{j} \to \frac{1}{\sqrt{N}} \sum_{k=0}^{N-1} e^{2 \pi ijk/N} \Ket{k}.
\end{equation}
For a general initial state $\sum_{j=0}^{N-1} c_j \Ket{j}$, the quantum Fourier transform performs as 
\begin{equation}
\sum_{j=0}^{N-1} c_j \Ket{j} \to \sum_{k=0}^{N-1} \tilde{c_k} \Ket{k}, \quad where \quad \tilde{c_k} = \frac{1}{\sqrt{N}} \sum_{j=0}^{N-1} e^{2 \pi ijk/N} c_j.
\end{equation}
%波浪模板
Before moving on, I will first prove that quantum Fourier transform is a unitary operation, which is a requirement for quantum gates.
\begin{claim}
Quantum Fourier transform is a unitary transformation.
\end{claim}

\begin{proof}
For clarity reasons, first I will rewrite the transform in outer product forms:
\begin{equation}
    F= \sum_{j=0}^{N-1} \sum_{k=0}^{N-1} \frac{e^{2 \pi ijk /N}}{\sqrt{N}} \ket{k}\Bra{j}.
\end{equation}
Consider 
\begin{equation}
\begin{split}
    {F^{\dag}}F & = \Big(\sum_{j=0}^{N-1} \sum_{k=0}^{N-1} \frac{e^{-2 \pi ijk /N}}{\sqrt{N}} \Ket{j}\Bra{k} \Big)      \Big(\sum_{j^{'}=0}^{N-1} \sum_{k^{'}=0}^{N-1} \frac{e^{2 \pi ijk /N}}{\sqrt{N}} \Ket{k'}\Bra{j'} \Big) \\
    %\dag: adjoint 模板 
        & = \frac{1}{N} \sum_{j,k,j',k'} e^{2 \pi i  (j' k'-jk) /N} \Ket{j} \Bra{j'}  \delta_{k k'} \\
        & = \frac{1}{N} \sum_{j,k,j'} e^{2 \pi i  k(j' -j) /N} \Ket{j} \Bra{j'}.
\end{split}
\end{equation}
When $j=j'$, $ e^{2 \pi i  k(j' -j) /N} \equiv 1$, thus $\sum_{k} e^{2 \pi i  k(j' -j) /N}= N$; If $j\neq j'$, then $\sum_{k} e^{2 \pi i  k(j' -j) /N} = (1- (\frac{2 \pi (j'-j)}{N})^n )/(1- \frac{2 \pi (j'-j)}{N} ) =0$.

In summary,
\begin{equation}
 \frac{1}{N} \sum_{j,k,j'} e^{2 \pi i  k(j' -j) /N} \Ket{j} \Bra{j'}  = \sum_{j,j'} \Ket{j} \Bra{j'} \delta_{j j'} = \sum{j} \Ket{j} \Ket{j} = I.
\end{equation}
Thus $F$ is a unitary operation. 
\end{proof}

Another more useful representation of the algorithm utilizes the binary representation of quantum states: Assume the computational basis are of dimension $N = 2^n$, then a state $\Ket{j}$ may be decomposed as $j = j_1 2^{n-1} + \dots + j_n 2^0$, and represented as $j = j_1 \dots j_n$. 

Using tensor products to dissemble each binary bits into individual qubits, we may get the product representation of quantum Fourier transform:

\begin{equation} \label{binary} 
\begin{split}
\Ket{j} & \to \frac{1}{2^{N}} \sum^{2^n-1}_{k=0} e^{2 \pi ijk/N} \Ket{k}\\
        & =  \frac{1}{2^{N}} \bigotimes_{l=1}^{n} \ [\Ket{0} + e^{2 \pi ij 2^{-l}} \Ket{1}]. %单个空格模板
\end{split}
\end{equation}  

It can be seen that if the system starts from the state $\Ket{j_1 \dots j_n}$, we can use some Hadamard gates and general phase-shift gates to complete the algorithm. A concrete example is integrated into the next section for a more general illustration.  

\subsubsection{Phase Estimation}

The phase estimation algorithm enables us to find the eigenvalue of a unitary operator $U$. First I will phrase the problem: Let $U$ be a unitary operator acting on $m$ qubits with an eigenvector $ |\psi \rangle $ and eigenvalue $ e^{2\pi i\theta} $ such that $ U|\psi \rangle =e^{2\pi i\theta }\left|\psi \right\rangle (0\leq \theta <1)$, where the value $\theta$ is to be determined. 

The algorithm contains two registers: The first ensemble contains t qubits, whose initial state is $\Ket{000 \dots}$, and the number $t$ depends on the expected estimation accuracy of $\theta$; The second register is initialized to an eigenstate of $U$. 

\begin{equation}
\Qcircuit  @C=1em @R=2em {
\lstick{\Ket{0}}& \gate{H} & \qw &                   \dots &&\ctrl{3}  & \multigate{2}{QFT^{-1}} &\meter &\qw \\
& \vdots & &&&&& \vdots \\
\lstick{\Ket{0}}& \gate{H} & \ctrl{1}&               \dots && \qw       &    \ghost{QFT^{-1}} &\meter &\qw \\
\lstick{\Ket{\psi}}&\qw \backslash^{m} & \gate{U} &  \dots && \gate{U^t}  &                   \qw    &\qw 
}
\end{equation}  %省略, slash, 测量模板
Phase estimation procedure contains two steps. First, each qubit in the first register is super-positioned using Hadamard gate.  Then controlled-$U$ operations are applied to the second register, with times of increasing powers of two. The output state is 
\begin{equation}
 \frac{1}{2^{N}}(\Ket{0} + e^{2 \pi i2^{t-1}\theta}\Ket{1})(\Ket{0} + e^{2 \pi i2^{t-2}\theta}\Ket{1}) \dots (\Ket{0} + e^{2 \pi i2^{0}\theta}\Ket{1}).
\end{equation}

Then the inverse quantum Fourier transform (the reverse procedure of the quantum Fourier transform) is applied to the first register, and the output state is
\begin{equation}
 \frac{1}{2^{N}}\sum^{2^t-1}_{j=0} \sum^{2^t-1}_{k=0} e^{-2 \pi ikj/2^t} e^{2 \pi i k \theta } \Ket{j}.
\end{equation}
If we measure the state of the first register,  then we can obtain $\theta$ to $n$ bits with chance of success at least $1- \epsilon$ if the number $t$ satisfies
\begin{equation}
t = n + \left \lceil{\log (2 + \frac{1}{2\epsilon})}\right \rceil. %ceiling 函数模板
\end{equation}
More generally, if the second register is not initially in an eigenstate of $U$, say the state of the register is $\Ket{\psi}$, then we may expand this state in terms of
the eigenstates $\Ket{u}$ of $U$ $\Ket{\psi} = \sum c_u \Ket{u}$. Suppose the eigenstate $\Ket{u}$ has eigenvalue $e^{2 \pi i \phi_u}$, then measuring the first register will give us with probability $|c_u|^2 $ the eigenstate $\Ket{u}$'s corresponding phase $\psi_u$.

\subsubsection{A concrete example} \label{PHASE}
Next let's consider a quantum circuit illustrating the phase estimation scheme using part of the circuits from \cite{EXP}. Below I will give the mathematical deduction of the quantum states involved:
\begin{equation}
    \Qcircuit @C=1em @R=2em {
\lstick{\Ket{0}} & \gate{H} &\qw          &\ctrl{2}         &\qw&\qswap     &\qw        &\gate{S^{-1}} &\gate{H}   &\meter     &\qw \\
\lstick{\Ket{0}} & \gate{H} &\ctrl{1}     &\qw              &\qw&\qswap \qwx&\gate{H}   &\ctrl{-1}     &\qw      &\meter     &\qw \\
\lstick{\Ket{u}} & \qw      &\gate{U}     &\gate{U^2}       &\qw&\qw        &\qw        &\qw           &\qw          &\qw        &\qw
}
\end{equation}
\bigskip
First, Hadamard gates and the controlled operations transform inject increasing length of bits of the eigenvalue of the operator $U$ into the first two registers. Then inverse Fourier transform is applied to the first two qubits to filter the phase factor. If then we measure the state of the qubits, we can get an approximation of the phase. 

Here the operator $U$ acts on the eigenstate $\Ket{u}$ as $U\Ket{u} = e^{2\pi i \phi} \Ket{u}$, and the term $\phi$ is the phase to be determined. In binary representations, $\phi$ may be written as $\phi = 0.\phi_1 \phi_2 \dots$, and the circuit operates as follows:
\begin{equation}
    \begin{split}
        \Ket{00u}   &\to \frac{1}{2}[\Ket{0}\Ket{0}\Ket{y} +\Ket{0}\Ket{1} e^{2 \pi i \phi} \Ket{y} +\Ket{1}\Ket{0}e^{2 \pi i \times 2 \phi} \Ket{y} + \Ket{1}\Ket{1}e^{2 \pi i \times 3 \phi}\Ket{y}]\\[10pt] %行距控制模板
                    & \qquad = \frac{1}{2}\big[ \Ket{0} + e^{2 \pi i 0.\phi_1 \dots} \big] \otimes \big[ \Ket{0} + e^{2 \pi i 0.\phi_2 \dots} \big] \otimes \Ket{y} \quad \text{after $U$ gates} \\[10pt]
                    & \to \frac{(1+e^{2 \pi i 0.\phi_1 \dots})(1+e^{2 \pi i 0.\phi_2})}{4} \Ket{00} + \frac{(1-e^{2 \pi i 0.\phi_1 \dots})(1+e^{2 \pi i 0.\phi_2})}{4} \Ket{10} \dots \\[10pt]
                    & \qquad + \frac{(1- i e^{2 \pi i 0.\phi_1 \dots})(1-e^{2 \pi i 0.\phi_2})}{4} \Ket{01} + \frac{(1+i e^{2 \pi i 0.\phi_1 \dots})(1-e^{2 \pi i 0.\phi_2})}{4} \Ket{11}
    \end{split}
\end{equation}
In general, none of the four coefficients corresponding to different states is zero, and thus we can only correctly extract the first two bits of the phase $\phi$ with accuracy 
\begin{equation}
    |c|^2 = \Bigg|\frac{(1+e^{\frac{\pi i }{2} 0.\phi_3 \dots})(1+e^{\pi i 0.\phi_3 \dots})}{4}\Bigg|^2.
\end{equation}
In the special case when $\phi=0.\phi_1 \phi_2=0.01$, we can immediately get that the state after the inverse Fourier transform is $\Ket{0}\Ket{1}\Ket{y}$, and thus the measurement yields $0$ and $1$ individually, as desired.

\section{Quantum Computer Realization}
Besides building quantum algorithms superior to their classical counterparts, experimentally realizing large-scale quantum computers is another obstacle to harnessing the power of quantum computation. Indeed, the main requirements to realize quantum computation include: \cite{QC2}
\begin{enumerate}
    \item Find a well-behaved system with characterized qubits to represent quantum information.
    \item Manipulate the state of the qubits into a fiducial state (such as $\Ket{000}$).
    \item Conduct a broad/complete family of unitary operations.
    \item Long enough significant decoherence time to do gate operations.
    \item Acquire a measurement method with high-fidelity.
\end{enumerate}   

In this report, I will focus on the realization method based on nuclear magnetic resonance(NMR) processors.
\subsection{Nuclear Magnetic Resonance}
NMR - based quantum computation is performed over a system of spin-$\frac{1}{2}$ nuclei (the qubits) of molecules in some solution. In the following, I will first introduce the Hamiltonian governing the states of the nuclei, and then how quantum computation can be implemented with NMR will be summarized.
\subsubsection{Hamiltonian of the system}
Quantum mechanics has shown that for a single spin-$\frac{1}{2}$ nucleus, its Hamiltonian in a static magnetic field $\mathbf{B_0}$ is $H_0 =- \mathbf{\mu} \cdot \mathbf{B_0} = − \gamma \mathbf{S} \cdot \mathbf{B_0}$, where $\gamma$ is the gyromagnetic ratio of the nucleus and $\mathbf{\mu} = \gamma \mathbf{S}$ its magnetic moment, $\mathbf{S} = \frac{1}{2} \mathbf{\sigma}$ being the spin operator.

In practice, a quantum register is represented by several spin-$\frac{1}{2}$ atomic nuclei (the qubits) in a molecule. Due to the shielding effects by other electrons with different degrees, generally we may denote the Hamiltonian for an n-qubit non-interacting molecule as follows(the system is in a static magnetic field directed along z):
\begin{equation}
    H_0 = - \sum_{i=1}^{n} {(1- \alpha^i)\gamma^i ~ B_0 S_z^i} = \sum_{i=1}^{n} \omega_0^i S_z^i
\end{equation}
If the scalar-coupling effect is also taken into consideration, then the total Hamiltonian for a system with n qubits of coupled nuclear spins is
\begin{equation}
    H_{sys} = \sum_{i} {\omega_0^i S_z^i} + \frac{2 \pi}{\hbar} \sum_{i<j} J_{ij} S_z^i S_z^j,
\end{equation}
where $J_{ij}$ reflects the coupling strength between the $i$th and $j$th nuclei. 
\subsubsection{Measures to represent quantum computing}

In this section, we focus on three aspects regarding utilizing NMR systems to perform quantum computing: preparing initial states, performing unitary operations and measuring output states.

It is well known that for a two-state system, the transition between the states are governed by Schrodinger's Equation. If we denote the energy difference between the two spin states (normally denoted as $\Ket{0}$ and $\Ket{1}$) is $\hbar \omega_0$, then we may manipulate the transition by applying an external magnetic field with frequencies near $\omega$. Especially at resonance frequency ($\omega = \omega_0$), the states are governed by the Hamiltonian $H = g_1(t) X+ g_2(t) Y$, where $g_1$ and $g_2$ are function of the applied field. In summary, the introduced Hamiltonian enables us to perform unitary manipulation on the spin-states which thus satisfies the requirement of quantum computing.

\bigskip
\noindent The preparation of initial states on an NMR system: NMR machines are operated under room temperature, and thus the initial state of nuclei is under the thermal equilibrium state $\rho = e^{- \frac{\beta H}{\mathcal{Z}}} $,  where $\beta = \frac{1}{k_BT}$, and $\mathcal{Z}= Tr[e^{−\beta H}]$ is the partition function. Under room temperature, the NMR state is approximated by $\rho = 2^{-n} [1- \beta H] $. The diagonal terms are dominant in the $Z$ basis, and thus the matrix is interpreted as the mixture of the pure states $\Ket{000} \dots \Ket{111}$. Then temporal labeling method transforms the mixed state into a pseudo-pure state.

\bigskip
\noindent Performance of unitary operations: as explained above, when a large RF field is applied at a proper frequency, the time evolution operator can be approximated by to a good approximation, we can approximate $e^{−iHt/\hbar} \approx e^{−iH_{RF}t/\hbar}$. The arbitrary Hamiltonian allows us to perform arbitrary single qubit operations. 

\bigskip
\noindent Readout Scheme: Instead of performing standard measurements which will collapse the entangled quantum states, the readout scheme in NMR is continuous and nondestructive, and the output induced in the coils is $V^{k} (t)= V_0 Tr[\rho(t) \sigma_{x,y}^k]$, where $\rho(t)$ is the density matrix, and the Pauli matrix operate on the k-th spin.  


\subsubsection{Properties of NMR systems}
NMR system has many features distinct from other quantum computation apparatus, for example,
\begin{enumerate}
    \item Instead of measuring the output from a single copy of quantum register, we average over
a large number of molecules to read the magnetization signal.
    \item The experiment is conducted at room temperature, and thus on highly mixed (thermal) states rather than pure states.
    \item The interaction between qubits is persistent, so that the Hamiltonian evolution due to undesired couplings has be removed manually (by refocusing techniques).
\end{enumerate}

\noindent Nevertheless, NMR systems are still of particular interest, as many quantum algorithms and quantum properties including entanglement have been implemented and confirmed through NMR systems. Next we will discuss one particular experimental realization.


\section{Application: NMR computer and quantum support vector machines}\label{EXP-F}
In this section, we discuss an experimental realization of a quantum algorithm – quantum support vector machine\cite{EXP}. First the scheme of the experiment will be explained, and then some discussions on the experiment will be proposed.

\subsection{General Theory} 
The experiment tries to classify digits (in this paper, the digits 6 and 9) using a quantum machine learning algorithm – support vector machine. First, digits are represented by feature vectors, and the classification result are represented by variable $y(=\pm 1)$, where that of 6 is denoted as ``positive`` (y=1) and that of 9 ``negative``. The algorithm completes the task to classify the class of a vector $\vec{x_0}$, i.e., decide the value of the corresponding variable $\vec{y_0}$. 

The core of the algorithm is a hyperplane with $\vec{w} \cdot \vec{x} + b = 0 $, subject to the assumption that $\vec{w} \cdot \vec{x_i} + b \geq 1$ for $\vec{x_i}$ with positive classification results, and $\vec{w} \cdot \vec{x_i} + b \leq -1$ for negative ones. The normal vector  $\vec{w}$  is weighted sum of training vectors, i.e., 
\begin{equation}
\vec{w}=\sum_{i=1}^{M} \alpha_i \vec{x_i},
\end{equation}
where M is the number of training data, and in this paper M=2. The machine learning comes exactly from the objective to optimize $\vec{w}$ and $b$ so that the distance between two classes($2/|\vec{w}|$) is maximal.

\begin{figure}[H] % 图片模板
\centering
\includegraphics[scale=1]{vec}
\caption{Illustration of support vector machines. \cite{VEC}}
\label{VEC-P}
\end{figure}

The parameters\space $\vec{w}$ \space and $b$ can be acquired by solving the equation 
\begin{equation}
    \tilde{F} (b,\alpha_{1},..., \alpha_{M})^T = (0, y_1,...,y_M)^T
\end{equation} 
following the least-squares approximation of SVM\cite{SVM}. $\tilde{F}$ is a $(M + 1) \times (M +1) $ matrix $K$ entailing the similarity between the vectors. In this experiment, the intercept b is set to zero, thus the matrix is reduced to $dim(F) = M \times M$, and in this case $2 \times 2$. 

\begin{figure}[H] % 图片模板
\centering
\includegraphics[scale=0.9]{exp}
\caption{Experiment Scheme of Quantum SVM \cite{EXP}}
\label{EXP-P}
\end{figure}

\bigskip
\noindent The whole algorithm contains roughly three parts: 
\begin{enumerate}  %point form, 列表 模板
    \item Preparing the pseudo-pure state of the quantum system (which will not be discussed here),
    \item extracting the feature vectors of both training and testing images, and preparing the  kernel matrix $K$,
    \item acquiring the hyperplane parameters $\vec{w}$ and classifying testing images. 
\end{enumerate}

The original paper illustrated the state flows with equations, and below I will fill in the explicit values of the matrices and quantum states for clarity and further discussion.

\subsection{Numerical Analysis}

First the feature vectors of the training data is encoded into two qubits to extract information about the density matrix $K$ and the matrix $F$ to be inverted, and we may get from Section \ref{PRE},
\begin{small}

\begin{equation}
    K = \begin{bmatrix}
   0.99945  & 0.49806 \\
   0.49806  & 0.99954
    \end{bmatrix},
    F = \begin{bmatrix}
                         1.49945 &	0.49806 \\
                         0.49806 &	1.49954
    \end{bmatrix}.
\end{equation} 
\end{small}
\bigskip
\noindent Next I will first give the result of the matrix inversion through classical methods, and then discuss the quantum approach for verification and comparison.

The matrix $F$ may be decomposed by $F=V D V^{-1}$, where $V$'s columns are eigenvectors and $D$'s diagonal terms are eigenvalues:
\begin{small}
\begin{equation}
F= \begin{bmatrix}
  -0.70714  & 0.70707 \\
   0.70707  & 0.70714
\end{bmatrix}
\begin{bmatrix}

   1.00143  &                 0 \\
                   0  & 1.99755
\end{bmatrix}
\begin{bmatrix}
  -0.70714  & 0.70707 \\
   0.70707  & 0.70714
\end{bmatrix},
\end{equation}
\end{small}
and as the value \begin{small}$\mathbf{b} = \begin{bmatrix}
  1 \\
  -1
\end{bmatrix}$ \end{small}, the hyperplane parameters are 

\begin{small} %使字体变小模板
\abovedisplayskip=1pt %使间距变小模板
\belowdisplayskip=1pt
\begin{equation}
  \mathbf{a}=  \begin{bmatrix}
  a_1 \\
  a_2
\end{bmatrix}
= \frac{1}{\sqrt{2}} \begin{bmatrix}
  1 \\
  -1
\end{bmatrix}.
\end{equation}
\end{small}

\begin{figure}[H] % 图片模板
\centering
\includegraphics[scale=0.6]{circuit}
\caption{The quantum circuit for classification \cite{EXP}}
\label{whole}

\end{figure}
\bigskip
\noindent Next I will discuss the approach of matrix inversion circuit:

First we decompose $\Ket{b}$ in the eigenvector basis 
\begin{small}
\begin{equation}
    \Ket{b} = \beta_1 \Ket{v_1} + \beta_2 \Ket{v_2} = -0.99999 \begin{bmatrix}
      -0.70714 \\
0.70707
    \end{bmatrix} 
  -0.00005 \begin{bmatrix}
    0.70707\\
0.70714
  \end{bmatrix},
\end{equation}
\end{small}
using the results in Section \ref{PHASE}, we get the state after Fourier transformation,
\begin{small}
\begin{equation}
    \sum_{\psi_1,\psi_2=0}^{1}  \Big{[} \textstyle {\sum} \alpha_{\psi_1 \psi_2 | \beta_i}\beta_i \Ket{v_i} \Big{]}  \Ket{\psi_1}\Ket{\psi_2},
\end{equation}
\end{small}
whose coefficients are, 
\begin{center}
 \begin{tabular}{||c | c||} 
 \hline
 $\alpha_{\psi_1 \psi_2 |\beta_1}$ & $\alpha_{\psi_1 \psi_2 |\beta_2}$ \\ [0.5ex] 
 \hline
  $-0.001127600504415 + 0.001120014228117i$ & $-0.000000000503854 - 0.000000087585601i$ \\
 \hline
 $-0.999991138328462 - 0.003375226617191i$ &  $0.000000087249051 - 0.000000088258696i$ \\
 \hline
 $0.001122537281808 + 0.001130140647694i$ &  $-0.000045675776705 + 0.000000262759379i$\\
 \hline
 $-0.000003797405739 + 0.001125071741380i$ &   $-0.000000087920863 - 0.000000086915082i$. \\
 \hline
\end{tabular}
\end{center}
It can be immediately spotted that, the only nontrivial term in the superposition states is $\Ket{\psi_1 \psi_2 | \beta_1} = \Ket{0} \Ket{1} \Ket{\beta_1}$.

Rotating conditioned on the Fourier basis states, and then uncomputing the circuits \cite{HHL}, we may get the state 
\begin{small}
\begin{equation}
    \sum \alpha_{\psi_1 \psi_2 | \beta_i}\beta_i \Ket{\psi_1}\Ket{\psi_2} \Ket{v_i} \big(\sqrt{1- \frac{C^2}{\lambda_j^2}}\Ket{0} + \frac{C}{\lambda_j}\Ket{0} \big),
\end{equation}
\end{small}
\begin{center}
 \begin{tabular}{||c | c||} 
 \hline
 $\alpha_{\psi_1 \psi_2 |\Ket{0}}$ & $\alpha_{\psi_1 \psi_2 |\Ket{1}}$ \\ [0.5ex] 
  \hline
$-0.5303067744762 + 0.1744070949332i$ &	$-0.7071005150385 - 0.002386645629057i$ \\
 \hline
$-0.1767951937665 - 0.17636319424662i$&	 $-3.508345439  e^{-6} + 0.00103943075446800i$ \\
 \hline
$-0.1768010459975 - 0.1746293316798i$&	 $-1.454841077 e^{-6} + 0.000431031261037493i$ \\
 \hline
$0.1767105347122 + 0.1767934597212i$ &	 $0.000431031261037493 + 1.454841077 e^{-6} i$.   \\
 \hline
\end{tabular}
\end{center}
It is worth mentioning that the circuit is successful conditioning on the fourth qubit reducing into $\Ket{1}$, thus the first column's nontrivial results have no influence on the result, and the second column, parameters for $\alpha_{\psi_1 \psi_2 |\Ket{1}}$, concentrates on the state $\Ket{0}\Ket{0}$, whose fidelity is $(1-3 \times 10^{-6})$.

Moreover, the matrix inversion result is $\vec{a}=0.99912\Ket{v_1} + 0.04197 \Ket{v_2}$, which approximates to our result using classical methods. 

Again calling the training-data oracle, from Section \ref{PRE}, the training-data state is $\Ket{u} = \sum_{i=1}^{2} |x_i| \alpha_i \Ket{i} \Ket{\vec{x_i}}$ and the query state is $\Ket{v} = \sum_{i=1}^{2} |x_0| \Ket{i} \Ket{\vec{x_0}}$ up to normalization. The inner product of the two states gives the prediction result by its sign.
%curr

\subsection{Discussion}

By simple algebra, we can show that for a matrix of the form $A=\begin{bmatrix}
  m \quad n\\
  n  \quad m
\end{bmatrix}$, the solution to the equation $A \vec{x}= \vec{b}$ is always $\vec{x}=\frac{1}{\sqrt{2}}\begin{bmatrix}
  1 \\
  -1
\end{bmatrix}$, i.e., the vector $\vec{b}$ is an eigenvector of the matrix $A$, thus the matrix inversion part did not show its function here. However, this is not the general case for classification with larger training sets or feature vectors.
\bigskip

\noindent Furthermore, from previous analysis we have seen that, the eigenvalues of the operator are $i$ and $-1$ individually, thus the phases can be represented accurately by $\phi_1=0.01$, $\phi_2 = 0.10$ as introduced in Section \ref{PHASE}. However, in practical classification scenarios, the phase factors can not be represented by the simple two bits, thus phase estimation algorithm tells us that accurate prediction may require much more qubits in the training register. This can also been seen from the requirement in \cite{HHL}: the evolution times T has to be large enough to make sure that one of the Fourier basis states will capture the phase $\phi$ to a great accuracy.

\subsection{Modification to classifying characters '0' and 'o'}
Finally, we discuss another task of distinguishing the handwritten characters $0$ and o. The task can be quite difficult for humans, while machine learning methods may offer us some insights into the problem. Below I will continue to use the support vector machine method to deal with the task. Apparently the left/right and up/down ratio used in the previous paper \cite{EXP} is not suitable here due to the symmetric behaviors of the two objects. Instead, I introduced the parameter $\Delta y/\Delta x$, which is the farthest vertical distance over the horizontal distance, and the parameter circum-radius over inscribed-radius $R_o /R_i$ to represent the feature of the handwritten characters.

\begin{figure}[htbp]
\centering
\begin{minipage}[t]{0.3\textwidth}
\centering
\includegraphics[width=100pt]{hand.jpg}
%\caption{Illustration of the parameters}
\end{minipage}
\begin{minipage}[t]{0.3\textwidth}
\centering
\includegraphics[width=80pt]{im_0.png}
%\caption{Handwritten $0$}
\end{minipage}
\begin{minipage}[t]{0.3\textwidth}
\centering
\includegraphics[width=80pt]{im_o.png}
%\caption{Handwritten o}
\end{minipage}
\caption{$1$:Illustration of the parameters. $2$: Handwritten'0'. $3$: Handwritten'o'. }
\end{figure}
Using the two parameters to vectorize hand-written images, I tested several training images, and the following distribution is found:
\begin{figure}[H] % 图片模板
\centering
\includegraphics[scale=0.6]{feature}
\caption{The features of training images. Blue dots represent '0', and orange dots represent 'o'.}
\label{feat}
\end{figure}
We can find that, the coefficients for '0' are larger than that for 'o' on both axes, which is in conformity with the definition of the two coefficients. Thus we can construct the decision boundary and normal vector $\vec{w}$. By using the same procedures as in the paper \cite{EXP}, we can train the support vector machine to classify the characters.
