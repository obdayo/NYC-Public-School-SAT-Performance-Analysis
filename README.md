# NYC-Public-School-SAT-Performance-Analysis
This project analyzes SAT scores from New York City public high schools to identify top-performing schools and uncover borough-level performance trends. The analysis helps educators, policymakers, and families understand how schools perform in key academic areas.

## Dataset
The dataset used, `schools.csv`, contains:
- `school_name`: Name of the high school
- `borough`: NYC borough where the school is located
- `average_math`: Average SAT math score (max 800)
- `average_reading`: Average SAT reading score (max 800)
- `average_writing`: Average SAT writing score (max 800)

## Objectives
- Identify schools with the best math SAT scores (>= 640).
- Determine the top 10 schools by combined SAT scores.
- Find the borough with the highest standard deviation in total SAT scores.

### Jupyter Notebook:
Open `SAT_Analysis_Notebook.ipynb` in JupyterLab or Jupyter Notebook, and run the cells step-by-step.

## 📈 Outputs
- `best_math_schools`: Schools with math scores ≥ 640.
- `top_10_schools`: Schools with highest combined SAT scores.
- `largest_std_dev`: Borough with the most score variability.
- Matplotlib bar charts for visual comparison.


# Import Libraries
import pandas as pd
import matplotlib.pyplot as plt

# Load Dataset
schools = pd.read_csv("schools.csv")
schools.head()

# Find Best Math Performing Schools
threshold = 0.8 * 800  # 80% of max math score
best_math_schools = schools[schools["average_math"] >= threshold]
best_math_schools = best_math_schools[["school_name", "average_math"]].sort_values("average_math", ascending=False)
best_math_schools.head()

# Top Math-Performing Schools
plt.figure(figsize=(10, 6))
best_math_schools.head(10).plot(kind="bar", x="school_name", y="average_math", legend=False)
plt.title("Top Math-Performing Schools (Score >= 640)")
plt.ylabel("Average Math Score")
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()

# Calculate Total SAT and Find Top 10 Schools
schools["total_SAT"] = schools["average_math"] + schools["average_reading"] + schools["average_writing"]
top_10_schools = schools.sort_values("total_SAT", ascending=False).head(10)[["school_name", "total_SAT"]]
top_10_schools

# Visualization: Top 10 Schools by Total SAT
plt.figure(figsize=(10, 6))
top_10_schools.plot(kind="bar", x="school_name", y="total_SAT", legend=False, color="green")
plt.title("Top 10 Schools by Combined SAT Score")
plt.ylabel("Total SAT Score")
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()

# Analyze Borough-Level SAT Score Variability
borough_stats = schools.groupby("borough")["total_SAT"].agg(
    num_schools="count",
    average_SAT="mean",
    std_SAT="std"
).reset_index()
borough_stats[["average_SAT", "std_SAT"]] = borough_stats[["average_SAT", "std_SAT"]].round(2)
borough_stats

# Borough with Highest Std Dev in SAT
largest_std_dev = borough_stats.sort_values("std_SAT", ascending=False).head(1)
largest_std_dev

# Visualization: SAT Standard Deviation by Borough
plt.figure(figsize=(8, 5))
borough_stats.sort_values("std_SAT", ascending=False).plot(kind="bar", x="borough", y="std_SAT", legend=False, color="orange")
plt.title("Standard Deviation of Total SAT Scores by Borough")
plt.ylabel("Standard Deviation")
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
