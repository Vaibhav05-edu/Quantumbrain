# Quantum Brain – Qubits vs Qumodes

This project explores **quantum-inspired feature extraction for brain voxel data** using two different paradigms:

- **Qubits (discrete-variable quantum circuits)**
- **Qumodes (continuous-variable quantum circuits)**

Both pipelines are implemented in parallel, each with **8 steps** from encoding to training and results.

---

# Pipeline Overview

# Step 1 – Encoding
- **Qubits**: Encode voxels with `RX` rotations.  
- **Qumodes**: Encode voxels with `Displacement`.

# Step 2 – Phase Variations
- **Qubits**: Added `RZ` per qubit.  
- **Qumodes**: Added `Rotation` per mode.

# Step 3 – Pairwise Entanglement
- **Qubits**: `CNOT + RZ` for correlations.  
- **Qumodes**: `TwoModeSqueezing` and optional `Beamsplitter`.

# Step 4 – Higher-order Correlations
- **Qubits**: Multi-qubit observables (`Z⊗Z`).  
- **Qumodes**: Heterodyne-style readout (`⟨X⟩`, `⟨P⟩`).

# Step 5 – Feature Extraction
- **Qubits**: Pauli-Z expectations.  
- **Qumodes**: Quadratures `[X0,P0,X1,P1,…]`.

# Step 6 – Neural Wrapper
- **Qubits**: Quantum feature map wrapped in `nn.Module` with trainable params.  
- **Qumodes**: Quantum extractor + classical regressor.

# Step 7 – Training
- **Qubits**: End-to-end differentiable with Torch.  
- **Qumodes**: Train regressor only (quantum side fixed).

# Step 8 – Results
- **Qubits**: Rapid convergence with quantum backprop.  
- **Qumodes**: Slower but consistent improvement.

---

 ##Comparison##

| Step              | Qubits (Discrete)                 | Qumodes (Continuous)                      |
|-------------------|-----------------------------------|-------------------------------------------|
| Encoding          | `RX`                             | `Displacement`                            |
| Phase Control     | `RZ`                             | `Rotation`                                |
| Entanglement      | `CNOT + RZ`                      | `TwoModeSqueezing`, `Beamsplitter`        |
| Higher Correl.    | `Z⊗Z` observables                | Heterodyne (X,P per mode)                 |
| Features          | Pauli-Z exps                     | Quadrature exps                           |
| Wrapper           | Quantum NN (trainable)           | Hybrid (quantum fixed + regressor)        |
| Training          | End-to-end with Torch gradients  | Classical regressor only                  |
| Results           | Loss ↓ from **4.8 → 0.7**        | Loss ↓ from **2.4 → 1.3**                 |

---


