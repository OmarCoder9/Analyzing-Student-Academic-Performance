# Analyzing Student Academic Performance

A comprehensive data cleaning and analysis project that processes student academic performance data, validates data quality, and derives meaningful educational metrics from raw student test scores.

## Table of Contents

- [Overview](#overview)
- [Project Structure](#project-structure)
- [Dataset](#dataset)
- [Data Cleaning Process](#data-cleaning-process)
- [Features & Derived Metrics](#features--derived-metrics)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Output](#output)

## Overview

This project aims to clean, validate, and enrich student academic performance data. It processes raw test scores across three subjects (Math, Reading, Writing) and generates meaningful insights through data quality checks and feature engineering.

**Key Features:**

- Comprehensive data cleaning and standardization
- Missing value and duplicate detection
- Outlier analysis using IQR method
- Automated grade assignment
- Performance metrics calculation
- Subject-level pass/fail determination

## Project Structure

```
.
├── data_cleaning.ipynb                      # Main Jupyter notebook with data pipeline
├── data/
│   ├── StudentsPerformance.csv              # Original raw dataset
│   └── student_performance_cleaned.csv      # Processed and cleaned dataset (output)
├── requirements.txt                         # Python dependencies
└── README.md                                # This file
```

## Dataset

### Source Data: `StudentsPerformance.csv`

The original dataset contains student performance records with the following attributes:

| Column                      | Description                                            |
| --------------------------- | ------------------------------------------------------ |
| gender                      | Student gender (male/female)                           |
| race/ethnicity              | Student racial/ethnic group (Group A-E)                |
| parental level of education | Highest education level of parents                     |
| lunch                       | Type of lunch program (standard/free/reduced)          |
| test preparation course     | Whether student completed prep course (completed/none) |
| math score                  | Math test score (0-100)                                |
| reading score               | Reading test score (0-100)                             |
| writing score               | Writing test score (0-100)                             |

## Data Cleaning Process

The data cleaning pipeline (`data_cleaning.ipynb`) performs the following steps:

### 1. **Data Loading & Inspection**

- Load the CSV file using pandas
- Display first few rows and dataset info
- Inspect column names and data types

### 2. **Column Standardization**

- Convert column names to lowercase
- Replace spaces with underscores
- Remove special characters
- Example: `Math Score` → `math_score`

### 3. **Data Type Normalization**

- Strip whitespace from string columns
- Convert to lowercase for consistency
- Handle special characters (e.g., replace "/" with "\_")

### 4. **Missing Values & Duplicates Check**

- Detect missing/null values per column
- Identify and count duplicate rows
- Status: No missing values or duplicates found in dataset

### 5. **Data Validation**

- Verify test scores are within valid range (0-100)
- Identify any invalid score entries
- Check for data consistency across subjects

### 6. **Outlier Detection**

- Use Interquartile Range (IQR) method for outlier detection
- Calculate Q1, Q3, and IQR for each score column
- Identify outliers beyond 1.5 × IQR bounds
- _Note: Outliers are identified but not removed to preserve data integrity_

### 7. **Feature Engineering**

- Create derived metrics for analysis
- Assign grades based on average scores
- Generate performance indicators

## Features & Derived Metrics

The cleaned dataset includes the following engineered features:

| Feature                                     | Description                                        |
| ------------------------------------------- | -------------------------------------------------- |
| `total_score`                               | Sum of all three test scores (0-300)               |
| `average_score`                             | Mean score across all subjects (0-100)             |
| `grade`                                     | Letter grade based on average score                |
| `math_pass`, `reading_pass`, `writing_pass` | Pass indicator per subject (threshold: 60)         |
| `all_subjects_passed`                       | Boolean: true if all subjects passed               |
| `score_std`                                 | Standard deviation of scores (consistency measure) |
| `score_range`                               | Difference between highest and lowest scores       |
| `strongest_subject`                         | Subject with highest score (math/reading/writing)  |
| `weakest_subject`                           | Subject with lowest score (math/reading/writing)   |

### Grade Scale

| Grade | Range |
| ----- | ----- |
| A     | ≥ 90  |
| B     | 80-89 |
| C     | 65-79 |
| D     | 50-64 |
| F     | < 50  |

## Requirements

- **Python** 3.7+
- **pandas** - Data manipulation and analysis
- **numpy** - Numerical computations
- **matplotlib** - Data visualization
- **seaborn** - Statistical data visualization

## Installation

1. **Clone or download the project:**

   ```bash
   cd Analyzing-Student-Academic-Performance
   ```

2. **Create a virtual environment (optional but recommended):**

   ```bash
   python -m venv .venv
   # On Windows:
   .venv\Scripts\activate
   # On macOS/Linux:
   source .venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

## Usage

1. **Open the Jupyter notebook:**

   ```bash
   jupyter notebook data_cleaning.ipynb
   ```

2. **Run the notebook cells sequentially:**
   - The notebook will load the raw dataset
   - Execute all data cleaning and validation steps
   - Generate derived features
   - Output the cleaned dataset

3. **Access the processed data:**
   - Output file: `data/student_performance_cleaned.csv`
   - Use this cleaned dataset for further analysis, visualization, or modeling

## Output

After running the notebook, you'll get:

1. **Cleaned Dataset** (`student_performance_cleaned.csv`)
   - All data quality issues resolved
   - Standardized column names and values
   - New engineered features added
   - Ready for analysis or machine learning

2. **Summary Statistics**
   - Dataset shape and dimensions
   - Grade distribution
   - Overall pass rate across all subjects
   - Outlier counts per subject

## Example Output

```
============================================================
FINAL DATASET SUMMARY
============================================================
Shape: (1000, 24)
Columns:
['gender', 'race_ethnicity', 'parental_level_of_education', ...]

Grade distribution:
A     150
B     250
C     350
D     200
F      50

Pass rate (all subjects): 87.5%
```

---

**Project Status:** Data cleaning and feature engineering pipeline completed. Ready for exploratory data analysis and modeling.

**Last Updated:** 2026
