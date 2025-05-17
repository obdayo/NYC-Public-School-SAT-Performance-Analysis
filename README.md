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
Open `NYC-Public-School-SAT-Performance-Analysis.ipynb` in JupyterLab or Jupyter Notebook, and run the cells step-by-step.

## 📈 Outputs
- `best_math_schools`: Schools with math scores ≥ 640.
- `top_10_schools`: Schools with highest combined SAT scores.
- `largest_std_dev`: Borough with the most score variability.
- Matplotlib bar charts for visual comparison.

