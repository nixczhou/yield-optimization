### Improving Yield with Anomaly Detection & Control Limit Tightening

1. Comparing ML Anomalies with Statistical Control Limits
If ML detects anomalies that are outside the initial (mean ± 3σ) statistical control limits, it confirms that those limits are reasonable.

If ML detects anomalies inside the initial control limits, it suggests that our statistical limits may need tightening.

Example:
Suppose our initial control limit for Parameter1 is (40, 60), but ML detects anomalies within the range (45, 55). This suggests that extreme values between 40-45 and 55-60 should also be treated as risky, so we adjust the control limits to a tighter range.

2. Data-Driven Control Limit Adjustment
Compute new boundaries based on non-anomalous data.

Instead of using mean ± 3σ, we use only the subset of "good data" (without anomalies) to recalculate control limits.

🔹 New UCL & LCL Calculation:
    LCL_{new} = Q1 - 1.5 \times IQR
    UCL_{new} = Q3 + 1.5 \times IQR
where IQR (Interquartile Range) is Q3 - Q1.

3. Process Optimization Using Anomaly-Free Data
Now that we have refined control limits, we ensure tunable parameters stay within these new, optimized boundaries.

This reduces process variations that negatively impact yield.

4. Implementation in Code
Let me modify the code to:

Recalculate control limits based on only non-anomalous data.

Optimize yield by recommending new parameter settings.
