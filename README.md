# 1st-minor-project

### 🔹 Project Overview
You’ll analyze NHANES body measurement data for adult males and females using NumPy, matplotlib, and basic statistics. Your goal: explore, visualize, and interpret gender-specific differences in anthropometric features and related health metrics.

---

### 🗂️ Section Guide & Key Implementation Steps

#### **1–2. Load the Data as NumPy Matrices**
- Use `numpy.loadtxt()` or `numpy.genfromtxt()` with `delimiter=','` and `skip_header=1` to load CSVs.
- Store them as `male` and `female` NumPy arrays.

#### **3. Weight Histograms (Subplots)**
- Use `matplotlib.pyplot.subplots(2, 1, figsize=(10, 8))`.
- Plot female weights on top, male below.
- Use `plt.xlim()` with min/max weight bounds covering both distributions for consistency.
  
#### **4. Boxplot Comparison**
- Extract `male_weights` and `female_weights` (i.e., column index `0`).
- Use `plt.boxplot([female_weights, male_weights], labels=['Female', 'Male'])`.
- Discuss center (median), spread (IQR), and outliers.
  
#### **5. Statistical Summaries**
- Use `np.mean`, `np.median`, `np.std`, `scipy.stats.skew`, `scipy.stats.kurtosis` for both genders.
- Include a Markdown interpretation: e.g., male weights are more skewed or dispersed.

#### **6. Add Female BMI Column**
- BMI = weight (kg) / (height (m))² → `height_cm / 100`
- Add this as an 8th column using `np.hstack()`.
  
#### **7. Standardise the Female Matrix**
- Compute z-scores per column: $$ z = \frac{x - \mu}{\sigma} $$
- Create `zfemale` using `scipy.stats.zscore` across axis 0.
  
#### **8. Scatterplot Matrix & Correlations**
- Use `pandas` for easier plotting with `seaborn.pairplot`.
- Compute both `pearsonr()` and `spearmanr()` for selected columns.
- Discuss linear vs monotonic trends between features (e.g., BMI vs waist).

#### **9. Add Ratio Columns**
- For both matrices, compute:
  - Waist-to-height: column[6] / column[1]
  - Waist-to-hip: column[6] / column[5]
- Use `np.column_stack()` to append.

#### **10. Boxplot: Ratio Comparison**
- Plot 4 boxplots: [female W/Ht, male W/Ht, female W/Hip, male W/Hip].
- Label clearly and interpret any gender-specific patterns.

#### **11. Health Metric Discussion (Markdown Only)**
- **BMI**: Easy to compute, but ignores fat distribution.
- **Waist-to-height ratio**: Better predictor of metabolic risk.
- **Waist-to-hip ratio**: Reflects central obesity but affected by body shape.

#### **12. Inspect Extreme BMI Cases**
- Use `np.argsort(female[:, 7])` to get lowest/highest BMI indices.
- Index into `zfemale` and `print()` 10 individuals.
- Discuss patterns: do high-BMI individuals show unusually high z-scores for waist or hip?
