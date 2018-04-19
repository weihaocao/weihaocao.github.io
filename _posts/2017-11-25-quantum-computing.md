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

## Qubits

Analogous to a classical bit in classical computers, a qubit is the basic two-level computational unit governed by quantum mechanics. It is represented as 

$$
| \psi \rangle = \alpha | 0 \rangle + \beta | 1 \rangle 
$$

It can be seen that rather than only take values 0 and 1 as in classical computers, the coefficients $$\alpha$$ and $$\beta$$ take continuous values. Unfortunately, measurement theory tells us that only one bit of information may be acquired when the state is measured, thus only state $$\mid 0 \rangle$$ or state $$\mid 1 \rangle$$ may be detected in experiments, and the coefficients cannot be acquired directly.
