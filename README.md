Solar Power Generation Data Analysis and Visualization

This project analyzes and visualizes solar power generation data from a 5-minute interval dataset using **Python**. The tool reads an Excel file containing power measurements, performs statistical analysis, visualizes the data, and allows filtering or searching specific power values.

---

Project Features

1. Data Loading
   - Reads an Excel file containing solar power generation data.
   - Handles missing values in the "Power(MW)" column.

2. statistical Analysis
   - Calculates:
     - Mean
     - Median
     - Mode
     - Standard Deviation
     - Variance
   - Provides a summary of:
     - Total number of measurements
     - Minimum power
     - Maximum power

3. **Data Visualization**
   - Plots power (MW) over time using `matplotlib`.
   - Provides a clear line graph for trend analysis.

4.Filtering and Searching
   - Allows users to filter power values above a user-defined threshold.
   - Allows users to search for a specific power value and returns the row indices if found.

---
Requirements

- Python 3.x
- Libraries:
  - `pandas`
  - `numpy`
  - `matplotlib`
- Excel file with a column named `"Power(MW)"
