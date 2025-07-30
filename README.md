# Quantum QR Code Generator with Encoded Message

This project provides a unique method for encoding a message into a QR code by leveraging principles of quantum computing. A user-provided message is processed through a quantum circuit, simulated using Qiskit, and the resulting quantum measurement is used in the QR code generation process.

## How It Works

The process combines classical data handling with a quantum algorithm to encode the message.

### Classical Processing

1.  **User Input**: A message string is provided by the user.
2.  **Preprocessing**: To create a unique character set, duplicate characters are removed from the message, and the result is sorted.
3.  **Binary Conversion**: The unique, sorted message is converted into a binary string by concatenating the 8-bit ASCII representation of each character.

### Quantum Processing

The Deutsch-Jozsa algorithm is at the heart of this project's quantum processing.

1.  **Quantum Circuit Setup**:
    * A `QuantumRegister` is established with a size equal to the length of the binary message, plus one ancillary qubit.
    * A `ClassicalRegister` is created, matching the length of the binary message.
    * These registers are then used to initialize a `QuantumCircuit`.
2.  **Superposition**:
    * An `X` gate flips the ancillary qubit to the `|1>` state.
    * A `Hadamard` gate is applied to all qubits, placing them in a superposition state.
3.  **Oracle**:
    * An oracle function marks the desired quantum state. This is achieved by applying a `CX` (CNOT) gate to the ancillary qubit for each qubit in the main register that corresponds to a '1' in the message's complementary binary string.
4.  **Measurement**:
    * `Hadamard` gates are applied once more to all qubits except the ancillary one.
    * The state of the qubits in the quantum register (excluding the ancilla) is then measured and recorded in the classical register.
5.  **Simulation**: The quantum circuit is executed on an `AerSimulator` to obtain measurement outcomes. The Deutsch-Jozsa algorithm ensures that the most probable measurement result is the original binary message string.

### QR Code Generation

The original message provided by the user is encoded into a standard QR code and saved as a `qr.png` image file.

## Usage

To run this notebook, you will need Python and the following libraries:

* qiskit
* qiskit-aer
* matplotlib
* qrcode

You can install these dependencies using pip:


pip install qiskit qiskit-aer matplotlib qrcode


After installation, run the cells in the Jupyter Notebook in sequence. You will be prompted to enter a message, and the script will generate the quantum circuit, perform the simulation, and save a QR code image.

## Output

* The measurement counts from the quantum simulation will be printed.
* A histogram that visualizes the measurement outcomes will be displayed.
* A QR code image named `qr.png` will be saved in the same directory.
* The secret binary code and the final measurement from the simulation will be printed.
