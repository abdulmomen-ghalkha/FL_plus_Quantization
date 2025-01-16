## Scenario Explanation: Communication Energy Consumption for FL Training with Quantization

This simulation calculates the total communication energy and the energy efficiency during training of FL models with quantization, by calculating the **achievable bit rate** for a set of users in a wireless communication system. Below is an explanation of the key parameters, the steps in the simulation, and the resulting insights.

### Parameters

1. **Number of Users** (`num_users = 20`): 
2. **Area Size** (`A = 10000 m^2`): 
    - Defines a 100 x 100 m^2 area in which the users are randomly located.
3. **Transmission Power** (`Pt = 100e-3 mW`):
4. **Bandwidth** (`B = 2e6` Hz):
    - The available bandwidth for the communication is 2 MHz.
5. **Noise Spectral Density** (`N0 = 1e-9` W/Hz):
6. **Model Size** (`32 * 1e6`): 
    - Assumes a model with parameters represented using 32 bits.
7. **Server Position**:
    - Fixed at the center of the area (500, 500), ensuring a centralized setup for communication.

### Achievable Bit Rate Calculation

- For each user, the bit rate is calculated using the **Shannon-Hartley theorem**: 

  <img src="https://i.upmath.me/svg/R_i%20%3D%20B%20%5Ccdot%20%5Clog_2%5Cleft(1%20%2B%20%5Cfrac%7BP_t%7D%7Bd_i%5E2%20%5Ccdot%20B%20%5Ccdot%20N_0%7D%5Cright)" alt="R_i = B \cdot \log_2\left(1 + \frac{P_t}{d_i^2 \cdot B \cdot N_0}\right)" />

  Where:
    - <img src="https://i.upmath.me/svg/R_i" alt="R_i" />: Bit rate for user <img src="https://i.upmath.me/svg/i" alt="i" />.
    - <img src="https://i.upmath.me/svg/P_t" alt="P_t" />: Transmission power.
    - <img src="https://i.upmath.me/svg/d_i" alt="d_i" />: Distance to the server.
    - <img src="https://i.upmath.me/svg/B" alt="B" />: Bandwidth.
    - <img src="https://i.upmath.me/svg/N_0" alt="N_0" />: Noise spectral density.

### Energy Comparison: Quantized vs. Full-Precision Model

To calculate the total energy required to achieve a target accuracy of 65% for both quantized and full-precision models, we first determine the number of training rounds needed. This is done by summing the rounds where the model's test accuracy is below the target accuracy, for both the quantized version and the full precision.

* <img src="https://i.upmath.me/svg/%5Ctext%7Btarget%5C_acc%5C_rounds%5C_quantized%7D%20%3D%20%5Csum_%7Bi%7D%20%5Cleft(%20%5Ctext%7Bavg%5C_test%5C_accs%5C_q%7D%5Bi%5D%20%3C%20%5Ctext%7Btarget%5C_acc%7D%20%5Cright)" alt="\text{target\_acc\_rounds\_quantized} = \sum_{i} \left( \text{avg\_test\_accs\_q}[i] &lt; \text{target\_acc} \right)" />
* <img src="https://i.upmath.me/svg/%5Ctext%7Btarget%5C_acc%5C_rounds%7D%20%3D%20%5Csum_%7Bi%7D%20%5Cleft(%20%5Ctext%7Bavg%5C_test%5C_accs%7D%5Bi%5D%20%3C%20%5Ctext%7Btarget%5C_acc%7D%20%5Cright)" alt="\text{target\_acc\_rounds} = \sum_{i} \left( \text{avg\_test\_accs}[i] &lt; \text{target\_acc} \right)" />

The energy required per round is given as:

* <img src="https://i.upmath.me/svg/%5Ctext%7BEnergy%20per%20round%7D%20%3D%20P_t%20%5Ctimes%20%5Ctext%7BTransmission%20Time%7D" alt="\text{Energy per round} = P_t \times \text{Transmission Time}" />

The total energy for the quantized model using 8 bits quantization is calculated as:

* <img src="https://i.upmath.me/svg/%5Ctext%7BTotal%20Energy%20(Quantized)%7D%20%3D%20%5Cfrac%7B%5Ctext%7Btarget%5C_acc%5C_rounds%5C_quantized%7D%20%5Ctimes%20%5Ctext%7BEnergy%20per%20round%7D%7D%7B4%7D" alt="\text{Total Energy (Quantized)} = \frac{\text{target\_acc\_rounds\_quantized} \times \text{Energy per round}}{4}" />

For the full-precision model:

* <img src="https://i.upmath.me/svg/%5Ctext%7BTotal%20Energy%20(Full%20Precision)%7D%20%3D%20%5Ctext%7Btarget%5C_acc%5C_rounds%7D%20%5Ctimes%20%5Ctext%7BEnergy%20per%20round%7D" alt="\text{Total Energy (Full Precision)} = \text{target\_acc\_rounds} \times \text{Energy per round}" />

Finally, the energy savings from using the quantized model is:

* <img src="https://i.upmath.me/svg/%5Ctext%7BEnergy%20Savings%7D%20%3D%20%5Cfrac%7B%5Ctext%7BTotal%20Energy%20(Full%20Precision)%7D%20-%20%5Ctext%7BTotal%20Energy%20(Quantized)%7D%7D%7B%5Ctext%7BTotal%20Energy%20(Full%20Precision)%7D%7D%20%5Ctimes%20100" alt="\text{Energy Savings} = \frac{\text{Total Energy (Full Precision)} - \text{Total Energy (Quantized)}}{\text{Total Energy (Full Precision)}} \times 100" />
