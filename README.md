# Improving Yield with Anomaly Detection & Control Limit Tightening

#### Idea
By removing anomalies and tightening control limits, aiming to reduce variability and improve yield.

#### 1. Comparing ML Anomalies with Statistical Control Limits
- **Scenario 1**: If ML detects anomalies **outside** the initial control limits (mean ± 3σ), it confirms that the limits are reasonable.
- **Scenario 2**: If ML detects anomalies **inside** the initial control limits, it suggests that the statistical limits may need tightening.

**Example**:  
- Initial control limit for `Parameter1`: (40, 60)  
- ML detects anomalies within the range (45, 55).  
- This implies that extreme values between 40–45 and 55–60 should also be treated as risky.  
- **Action**: Adjust the control limits to a tighter range.

#### 2. Data-Driven Control Limit Adjustment
- Recalculate boundaries using only non-anomalous data.
- Replace the traditional `mean ± 3σ` approach with a method based on "good data."

**New Control Limit Calculation**:  
- Lower Control Limit (LCL):  
    \[
    LCL_{new} = Q1 - 1.5 \times IQR
    \]
- Upper Control Limit (UCL):  
    \[
    UCL_{new} = Q3 + 1.5 \times IQR
    \]
    where \( IQR \) (Interquartile Range) = \( Q3 - Q1 \).

#### 3. Process Optimization Using Anomaly-Free Data
- Refined control limits ensure tunable parameters stay within optimized boundaries.
- This reduces process variations and improves yield.

#### 4. Implementation in Code
- Recalculate control limits using only non-anomalous data.
- Optimize yield by recommending new parameter settings.

#### More Approach:
- Dynamic control limits for changing processes
- Advanced anomaly detection algorithms (e.g., DBSCAN, Autoencoders).
- Multivariate control limits to account for parameter correlations.
    - Instead of calculating control limits for each parameter independently, use multivariate techniques to account for correlations between parameters.
    - Example: Use Principal Component Analysis (PCA) to reduce dimensionality and detect anomalies in the transformed space.
    -  ````python
        from sklearn.decomposition import PCA
        pca = PCA(n_components=2)
        transformed_data = pca.fit_transform(data.iloc[:, :-1])
        iso_forest = IsolationForest(contamination=0.05, random_state=42)
        data['PCA_Anomaly'] = iso_forest.fit_predict(transformed_data) == -1
        ````
- Bayesian optimization for direct yield maximization.
- Clustering-based control for pattern recognition.
 - Use clustering algorithms (e.g., K-Means) to group data into clusters and identify clusters with poor yield.
 - Define control limits based on the "good" clusters.

#### Which Method to Choose?
- If your process is stable: Your current method (statistical + Isolation Forest) is likely sufficient.
- If your process is dynamic: Consider dynamic control limits or Bayesian optimization.
- If parameters are correlated: Use multivariate techniques like PCA or clustering.
- If you want to explore alternatives: Try DBSCAN, One-Class SVM, or Autoencoders for anomaly detection.


---
**Note**: The above steps provide a systematic approach to improve yield by leveraging ML-based anomaly detection and data-driven control limit adjustments.
