# Improving Yield with Anomaly Detection & Control Limit Tightening

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

---
**Note**: The above steps provide a systematic approach to improve yield by leveraging ML-based anomaly detection and data-driven control limit adjustments.
