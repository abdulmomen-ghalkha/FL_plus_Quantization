# Scenario Explanation: Comunicaton Energy Consumption for FL Training with Quantization


This simulation calculates the total communication energy and the energy efficiency during when training of FL models with quantization, by calculating the **achievable bit rate** for a set of users in a wireless communication system. Below is an explanation of the key parameters, the steps in the simulation, and the resulting insights.

---

## **Parameters**
1. **Number of Users** (`num_users = 20`):

2. **Area Size** (`area_size = 10000 m^2`):
   - Defines a \(100 * 100  m^2) area in which the users are randomly located.

3. **Transmission Power** (`Pt = 100e-3 mW` ):

4. **Bandwidth** (`B = 2e6` Hz):
   - The available bandwidth for the communication is 2 MHz.

5. **Noise Spectral Density** (`N0 = 1e-9` W/Hz\):

6. **Model Size** (`model_size_bits = 32 * 1e6`):
   - Assumes a model with paramaters represented using \(32 bits\).

7. **Server Position**:
   - Fixed at the center of the area \(500, 500\), ensuring a centralized setup for communication.


---


## **Achievable Bit Rate Calculation**:
   - For each user, the bit rate is calculated using the **Shannon-Hartley theorem**:
     \[
     R_i = B \cdot \log_2\left(1 + \frac{P_t}{d_i^2 \cdot B \cdot N_0}\right)
     \]
     Where:
     - \(R_i\): Bit rate for user \(i\).
     - \(P_t\): Transmission power.
     - \(d_i\): Distance to the server.
     - \(B\): Bandwidth.
     - \(N_0\): Noise spectral density.



---
## Energy Comparison: Quantized vs. Full-Precision Model

To calculate the total energy required to achieve a target accuracy ($ \text{target_acc} $) of 65% for both quantized and full-precision models, we first determine the number of training rounds needed. This is done by summing the rounds where the model's test accuracy is below the target accuracy, for hte both the quantized version and the full precision.
$
\text{target_acc_rounds_quantized} = \sum_{i} \left( \text{avg_test_accs_q}[i] < \text{target_acc} \right)
$

$
\text{target_acc_rounds} = \sum_{i} \left( \text{avg_test_accs}[i] < \text{target_acc} \right)
$

The energy required per round is given as:

$
\text{Energy per round} = P_t \times \text{Transmission Time}
$

The total energy for the quantized model is calculated as:

$
\text{Total Energy (Quantized)} = \frac{\text{target_acc_rounds_quantized} \times \text{Energy per round}}{4}
$

For the full-precision model:

$
\text{Total Energy (Full Precision)} = \text{target_acc_rounds} \times \text{Energy per round}
$

Finally, the energy savings from using the quantized model is:

$
\text{Energy Savings} = \frac{\text{Total Energy (Full Precision)} - \text{Total Energy (Quantized)}}{\text{Total Energy (Full Precision)}} \times 100
$

This method quantifies the efficiency of quantization, which reduces energy consumption by lowering the computational and communication overhead while achieving the same target accuracy.