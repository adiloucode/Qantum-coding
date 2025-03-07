### Steps to Build Quantum Variational Classifier

0. **Define number of Qbits, and a device for the quantum approach**:

   - This simple classifier works with 2D data, so it can restrain to one Qbit
   - A hardware device must be selected for quntum operations, either a simulator (e.g., default.qubit (our choice), lightening.qubit for larger circuits, or qiskit.aer (deprcated))
   - Or a Quantum computer accessible via a cloud service (e.g., qiskit.ibmq, rigetti.qpu, ionq.qpu)
   - The device must be set to the correct number of qubits, in this case 1

1. **Data Preparation**:

   - Collect and preprocess your dataset, here I used generated data from scikit learn library
   - Normalize or standardize the data if necessary.

2. **Encoding Classical Data**:

   - Use a suitable encoding method (e.g., amplitude encoding, basis state encoding) to convert classical data into quantum states.In our case we used amplitude encoding.

3. **Implemeting Circuit**:

   - Implement a quantum circuit that can be trainable, in our case, we used a circuit formed of two gates, Ry to affect prbability and amplitude, and Rz to affect phase. parameters are then inserted to perform the weighted rotation

4. **Test your circuit (Optional)**:

   - To make sure the implementation is working correctly we tested on the first data point of our training sample

5. **Training the model (the parameters associated to the rotation gates within the circuit)**:

   - First define a loss function, ours made measurements all over traininf data and calculated the mean squared error
   - Chose an optimazer for weights adjustements, we opted for the Gradient descent optimizer from the qlm library
   - Train the model using the training data and the defined loss function and optimizer, and return final parameters as a numpy array.

6. **Prediction**:
   - Classify the test instance based on the measurement value, using a threshold for binary calssification (in our case, values range between [-1, 1], a suitable threshold would be 0).
