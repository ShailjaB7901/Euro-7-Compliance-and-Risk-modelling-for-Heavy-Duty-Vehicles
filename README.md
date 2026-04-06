# Euro 7 Compliance and Risk modelling for Heavy Duty Vehicles
As the European Union transitions from Euro 6 to the more stringent Euro 7 regulations (2027/2028), automotive manufacturers face a critical "Compliance Gap." This project utilizes a dataset of 250,000+ vehicle registrations to build a predictive "Digital Twin" of fleet emissions. By identifying the physical drivers of $CO_2$, the model provides a strategic roadmap for engineering priorities in the Mercedes-Benz heavy-duty segment.This project builds a Digital Twin to identify "Compliance Leaks" within the highest-risk segment: High-Mass Petrol Vehicles

## 2. The Challenge: The "Regulatory Cliff"

Stricter Durability: Euro 7 extends compliance requirements to 875,000 km for heavy trucks, making "Cold Start" and "Low-Load" emissions a massive financial liability.
The Data Blind Spot: Standard laboratory values (WLTP) often fail to show linear relationships across mixed fleets (EVs, Hybrids, ICEs). My analysis identifies these hidden "Compliance Leaks" before they trigger EU penalties.

## 3. Data Engineering & InsightsSegment Decoupling:

Initial analysis of the total fleet showed a near-zero correlation ($r = -0.01$) between mass and emissions.
The Breakthrough: By segmenting the data, a 0.88 correlation was discovered within the Petrol (ICE) segment ($n = 133,991$). This proved that for combustion-based transport, Vehicle Mass remains the primary engineering lever for decarbonization.

### Preprocessing: 
I implemented a robust pipeline including grouped imputation for missing engine data, target scaling to prevent gradient explosion, and feature normalization.

## 4. Technical Implementation (The "How")Architecture:

Developed a Deep Neural Network using PyTorch with a multi-layer perceptron (MLP) structure (32-16-1 hidden layers).
Optimization Strategy:Loss Function: Mean Squared Error (MSE).Stability: Utilized Gradient Clipping and Target Normalization to handle high-variance outliers in heavy-duty vehicle weights.
Validation: Employed an 80/20 train-test split to ensure model generalization.

## 5. Results & ImpactPredictive Accuracy: 

Achieved a Test R² Score of 0.9043, meaning the model explains over 90% of emission variance.

### Precision: 
Reached a Test RMSE of 17.81 g/km, providing a reliable baseline for "what-if" engineering simulations.

## 6. Risk Audit:

The "Financial Zombie" IdentificationUsing the model, I performed a stress-test on the Petrol/Armored segment to identify vehicles that are mathematically unviable under 2026/2027 regulations. A "Financial Zombie" is a vehicle where the projected EU $CO_2$ penalty exceeds the unit's operating profit.

### The Math:
With 2026 EU penalties at €95 per g/km over the target (93.6 g/km for cars/vans), a vehicle emitting 442 g/km (like the S 680 Guard) faces a penalty of approximately €33,100 per unit.

### Findings: 
The audit flagged 180,005 units as high-risk "Zombies." For the company, this represents a €3.87 Billion cumulative liability that threatens the projected 6%–8% Adjusted Return on Sales (ROS).


## 6. Conclusion & Future Scope:
The model successfully bridges the gap between static registration data and predictive engineering. For a manufacturer like Daimler Truck, this tool can be scaled to Predict RDE (Real Driving Emissions) by integrating high-frequency sensor data.Optimize Fleet Mix by simulating the $CO_2$ impact of adding new vehicle configurations before they hit the production line.Ensure Penalty Avoidance by forecasting the fleet-wide average against EU 2027/2030 targets.
