# Euro-7-Compliance-and-Risk-modelling-for-Heavy-Duty-Vehicles
As the European Union transitions from Euro 6 to the more stringent Euro 7 regulations (2027/2028), automotive manufacturers face a critical "Compliance Gap." This project utilizes a dataset of 250,000+ vehicle registrations to build a predictive "Digital Twin" of fleet emissions. By identifying the physical drivers of $CO_2$, the model provides a strategic roadmap for engineering priorities in the Mercedes-Benz heavy-duty segment.

# 2. The Challenge (The "Why")The Regulatory Shift: 
Euro 7 introduces stricter "Cold Start" requirements and real-world durability standards (up to 875,000 km for trucks).

## The Data Problem: 
Standard laboratory values (Ewltp) often fail to show a clear linear relationship across a mixed fleet (EVs, Hybrids, and ICEs), creating "blind spots" in compliance strategy.
## Objective:
Develop a high-precision Machine Learning model to predict $CO_2$ output based on vehicle design specifications (Mass and Displacement).

# 3. Data Engineering & InsightsSegment Decoupling:
Initial analysis of the total fleet showed a near-zero correlation ($r = -0.01$) between mass and emissions.
The Breakthrough: By segmenting the data, a 0.88 correlation was discovered within the Petrol (ICE) segment ($n = 133,991$). This proved that for combustion-based transport, Vehicle Mass remains the primary engineering lever for decarbonization.

## Preprocessing: 
I implemented a robust pipeline including grouped imputation for missing engine data, target scaling to prevent gradient explosion, and feature normalization.

# 4. Technical Implementation (The "How")Architecture:
Developed a Deep Neural Network using PyTorch with a multi-layer perceptron (MLP) structure (32-16-1 hidden layers).
Optimization Strategy:Loss Function: Mean Squared Error (MSE).Stability: Utilized Gradient Clipping and Target Normalization to handle high-variance outliers in heavy-duty vehicle weights.
Validation: Employed an 80/20 train-test split to ensure model generalization.

# 5. Results & ImpactPredictive Accuracy: 
Achieved a Test R² Score of 0.9043, meaning the model explains over 90% of emission variance.
## Precision: 
Reached a Test RMSE of 17.81 g/km, providing a reliable baseline for "what-if" engineering simulations.
## Strategic Risk Map: 
I created a Compliance Heatmap that visualizes the "Euro 7 Danger Zone." The model identified that high-mass variants (330+ g/km) are currently under-performing against targets, highlighting a need for immediate aerodynamic or powertrain optimization.

# 6. Conclusion & Future Scope:
The model successfully bridges the gap between static registration data and predictive engineering. For a manufacturer like Daimler Truck, this tool can be scaled to Predict RDE (Real Driving Emissions) by integrating high-frequency sensor data.Optimize Fleet Mix by simulating the $CO_2$ impact of adding new vehicle configurations before they hit the production line.Ensure Penalty Avoidance by forecasting the fleet-wide average against EU 2027/2030 targets.
