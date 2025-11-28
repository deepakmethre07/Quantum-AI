from qiskit import QuantumCircuit, transpile
from qiskit_aer import Aer
import numpy as np

# --- 1. Charlie (The Entangled Source) ---
def create_bell_state():
    """Creates a Bell state circuit (|Phi+> = 1/sqrt(2) * (|00> + |11>))."""
    qc = QuantumCircuit(2, 2)
    qc.h(0)
    qc.cx(0, 1)
    return qc

# --- 2. Alice and Bob's Measurement Bases ---
ALICE_BASES = [0, np.pi/4, np.pi/2]        # 0, 45, 90 degrees
BOB_BASES   = [np.pi/4, np.pi/2, 3*np.pi/4]# 45, 90, 135 degrees

def apply_measurement(circuit, qubit, basis_angle):
    """Applies a rotation to change the measurement basis then measures."""
    if basis_angle != 0:
        circuit.ry(-basis_angle, qubit)
    circuit.measure(qubit, qubit)
    return circuit

# --- 3. Protocol Simulation ---
def e91_simulation(num_bits):
    key_stream = []
    simulator = Aer.get_backend('qasm_simulator')

    for _ in range(num_bits):
        qc = create_bell_state()

        alice_basis_angle = np.random.choice(ALICE_BASES)
        bob_basis_angle   = np.random.choice(BOB_BASES)

        apply_measurement(qc, 0, alice_basis_angle)  # Alice measures qubit 0
        apply_measurement(qc, 1, bob_basis_angle)    # Bob measures qubit 1

        compiled_circuit = transpile(qc, simulator)
        job = simulator.run(compiled_circuit, shots=1)
        result = job.result()
        counts = result.get_counts(qc)

        measurement = list(counts.keys())[0]   # string like 'b_a'
        alice_result = int(measurement[1])     # qubit 0 mapped to classical bit 0 (right char)
        bob_result   = int(measurement[0])     # qubit 1 mapped to classical bit 1 (left char)

        # Classical post-processing (public channel)
        if alice_basis_angle == bob_basis_angle:
            # For |Phi+>, results are correlated (same), so no flip required.
            alice_key_bit = alice_result
            bob_key_bit   = bob_result   # <-- removed the incorrect flip (1 - bob_result)
            key_stream.append((alice_key_bit, bob_key_bit, "Key"))
        else:
            key_stream.append((alice_result, bob_result, "Check"))

    return key_stream

# --- 4. Running the Simulation ---
NUMBER_OF_QUBITS = 10
key_data = e91_simulation(NUMBER_OF_QUBITS)

print(f"--- E91 Protocol Simulation ({NUMBER_OF_QUBITS} Rounds) ---")
print("Alice's Bits | Bob's Bits | Purpose")
print("---------------------------------")
for alice_bit, bob_bit, purpose in key_data:
    print(f"    {alice_bit}        |     {bob_bit}      | {purpose}")
    if purpose == "Key":
        print(f"    (Match? {alice_bit==bob_bit})")
