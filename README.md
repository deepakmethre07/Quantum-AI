# 🔐 Quantum Cryptography Using the E91 Protocol  
*A simulation of quantum key distribution using entangled photon pairs.*

---

## 📌 Overview

This project demonstrates **Quantum Key Distribution (QKD)** using the **E91 protocol**, introduced by Artur Ekert in 1991.  
The E91 protocol uses **entangled photon pairs** and the **Bell Inequality** to securely generate a shared secret key between two parties (Alice and Bob).  

Unlike classical cryptography, the security here is guaranteed by **laws of quantum mechanics**, not computational hardness.

---

## 🎯 Key Features

- Simulates **entangled qubits** shared between Alice and Bob  
- Implements **random basis selection** for measurements  
- Applies **Bell Inequality (CHSH test)** for eavesdropper detection  
- Generates a **shared cryptographic key**  
- Detects if an attacker (Eve) tries to intercept qubits  
- Fully implemented using Python (NumPy / Qiskit / custom logic)

---

## 🔬 What Is E91 Protocol?

E91 is based on the concept of **quantum entanglement**:

- Alice and Bob receive **entangled photon pairs**
- They measure their particles using randomly selected bases
- Correlations of entangled states follow **quantum mechanics**
- An attacker (Eve) breaks these correlations  
  → So if the **Bell inequality is violated**, the channel is secure  
  → If not, **eavesdropping is detected**

---

## 🧠 How the Protocol Works (Simplified)

1. **Entangled photon pairs** are created (e.g., Bell state |Φ⁺⟩).  
2. One photon goes to **Alice**, the other to **Bob**.  
3. Both choose **random measurement bases**:  
   - Alice: A1, A2  
   - Bob: B1, B2  
4. They measure their photons and record results.  
5. They publicly share **only their measurement bases** (not outcomes).  
6. Matching basis pairs → used for **key generation**  
7. Mismatched basis pairs → used for **Bell Inequality test**  
8. If Bell test is satisfied → **secure**  
   Else → **Eve detected**

---

## 🧪 Technologies Used

- **Python**
- **NumPy** – vector/matrix calculations  
- **Qiskit** (optional) – simulating quantum circuits & Bell states  
- **Matplotlib** (optional) – plot Bell test results  

---

## 📁 Project Structure

