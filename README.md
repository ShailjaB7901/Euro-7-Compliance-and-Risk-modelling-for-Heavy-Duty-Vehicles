# Euro 7 Compliance and Risk modelling for Vehicles

## 1. Data Provenance & Pre-processing

The foundation of this audit is the European Environment Agency (EEA) official registry of New Passenger Cars. To ensure the model reflects the current technological and regulatory landscape, a multi-stage extraction and filtration pipeline was developed.

#### Data Source: Primary datasets were retrieved from the EEA’s Monitoring of $CO_2$ Emissions repository, covering a population of over 1.2 million vehicle registrations.

Temporal Filtering: The dataset was restricted to the 2022, 2023, and 2024 reporting cycles. This specific window was chosen to capture the transition to WLTP (Worldwide Harmonised Light Vehicles Test Procedure) standards, providing a high-fidelity baseline for 2026/2027 forecasting.

Manufacturer Focus: Filtered for Mercedes-Benz AG to align with corporate-specific emission profiles.


As the European Union transitions from Euro 6 to the more stringent Euro 7 regulations (2027/2028), automotive manufacturers face a critical "Compliance Gap." This project utilizes a dataset of 780,000+ vehicle registrations to build a predictive "Digital Twin" of fleet emissions. By identifying the physical drivers of $CO_2$, the model provides a strategic roadmap for engineering priorities in the Mercedes-Benz heavy-duty segment.This project builds a Digital Twin to identify "Compliance Leaks" within the highest-risk segment: High-Mass Petrol Vehicles

## 2. The Challenge: The "Regulatory Cliff"

Euro 7 introduces stricter and longer durability requirements, extending compliance up to 875,000 km for heavy-duty vehicles. This significantly increases the impact of cold-start and low-load emissions over a vehicle’s lifetime.
At the same time, standard laboratory metrics (WLTP) often fail to capture consistent relationships across mixed fleets (EVs, hybrids, and ICE vehicles), creating a critical data blind spot.
This project addresses that gap by identifying hidden compliance risks before they translate into financial penalties.

## 3. Data Engineering & Insights Segment Decoupling:

Initial analysis of the total fleet showed a near-zero correlation ($r = -0.01$) between mass and emissions.
The Breakthrough: By segmenting the data, a 0.88 correlation was discovered within the Petrol (ICE) segment ($n = 133,991$). This proved that for combustion-based transport, Vehicle Mass remains the primary engineering lever for decarbonization.

### Preprocessing: 
I implemented a robust pipeline including grouped imputation for missing engine data, target scaling to prevent gradient explosion, and feature normalization.

## 4. Technical Implementation (The "How") Architecture:

Developed a Deep Neural Network using PyTorch with a multi-layer perceptron (MLP) structure (32-16-1 hidden layers).
Optimization Strategy:Loss Function: Mean Squared Error (MSE).Stability: Utilized Gradient Clipping and Target Normalization to handle high-variance outliers in heavy-duty vehicle weights.
Validation: Employed an 80/20 train-test split to ensure model generalization.

## 5. Results & Impact Predictive Accuracy: 

Achieved a Test R² Score of 0.9043, meaning the model explains over 90% of emission variance.

### Precision: 
Reached a Test RMSE of 17.81 g/km, providing a reliable baseline for "what-if" engineering simulations.

## 6. Risk Audit:

The "Financial Zombie" IdentificationUsing the model, I performed a stress-test on the Petrol/Armored segment to identify vehicles that are mathematically unviable under 2026/2027 regulations. A "Financial Zombie" is a vehicle where the projected EU $CO_2$ penalty exceeds the unit's operating profit.

### The Math: 
Financial Risk Audit (2026 Strategy)To calculate the business impact, I benchmarked the fleet against Mercedes-Benz’s 2026 Financial Guidance, which targets an 8% Adjusted Return on Sales (RoS).

#### The Core Logic:The model identifies "Financial Zombies"—vehicles where the EU compliance penalty is higher than the unit’s profit.
Unit Profit: Estimated at €4,400 (8% margin on an average €55,000 retail price).
Compliance Debt: Calculated using the 2026 EU penalty rate of €95 per g/km for every gram above the 93.6 g/km target.

#### The "Zombie" Formula: $$\text{Penalty} = (\text{Actual } CO_2 - 93.6) \times 95$$  
If Penalty > €4,400, the vehicle is a net loss for the company.

#### Stress-Test Case: The S 680 Guard (Petrol V12)
Using the model on the heaviest petrol unit (4,255 kg) reveals the extreme financial risk
* Actual Emissions: 442 g/kmCalculated
* Penalty: €33,098 per unit
* The Verdict: This single vehicle creates a €33k compliance debt, which is 7.5x higher than the average unit profit.

### Findings: 
The audit flagged 180,005 units as high-risk "Zombies." For the company, this represents a €3.87 Billion cumulative liability that threatens the projected 6%–8% Adjusted Return on Sales (ROS).


## 6. Conclusion & Future Scope:
The model successfully bridges the gap between static registration data and predictive engineering, transforming $CO_2$ from a retrospective reporting metric into a proactive design variable.

### Key Project Outcomes:

#### The "Digital Twin" Breakthrough: By isolating the Petrol ICE segment, the model moved from a near-zero correlation ($r=-0.01$) to a high-precision $R^2$ of 0.90. This proves that mass remains the primary physical lever for emission control in combustion-based transport.

#### Financial Risk Mapping: The project transitioned from physics to finance by identifying "Financial Zombies"—units where EU penalties (averaging €33,000 for high-mass models) effectively negate the projected 8% profit margin.

#### Future Scope:
* Predictive Fleet Mixing: Scaling the model to simulate the $CO_2$ impact of adding new vehicle configurations before they hit the production line, ensuring the fleet-wide average stays below the 93.6 g/km target.
* Real-World Correlation (RDE): Integrating high-frequency sensor data to evolve this model from laboratory WLTP values to Real Driving Emissions (RDE), accounting for the stricter Euro 7 durability standards.
* Multi-Fuel Integration: Expanding the Neural Network architecture to include Diesel and Hybrid categories,  allowing for a total portfolio view of regulatory liability.
