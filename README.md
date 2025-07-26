# Analysis of SAT Scores in New York City High Schools

### Project Overview

This project conducts an in-depth analysis of SAT scores across high schools in New York City. By combining seven different datasets, including demographic information, class sizes, AP test results, and survey responses, this analysis aims to uncover the key factors that correlate with SAT performance. The SAT (Scholastic Aptitude Test) is a standardized test widely used for college admissions in the United States, making its fairness and the factors influencing its outcomes a critical area of study.

This project serves as a practical example of a complete data analysis workflow, from cleaning and merging disparate data sources to exploratory data analysis and insight generation.

---

### Key Questions

* Is the SAT a fair test? Do demographic factors like race, gender, or income correlate with performance?
* What is the relationship between school safety, as perceived by students and teachers, and academic outcomes?
* Does a higher rate of Advanced Placement (AP) exam participation in a school correspond to higher average SAT scores?
* Are there significant differences in SAT performance between different boroughs of New York City?

---

### Data Sources

The analysis integrates data from seven separate files provided by New York City:

1.  **SAT Scores:** `sat_results.csv` - SAT scores for each high school.
2.  **School Directory:** `hs_directory.csv` - General school information, including location.
3.  **Class Size:** `class_size.csv` - Information on class sizes.
4.  **AP Test Results:** `ap_2010.csv` - Advanced Placement exam results.
5.  **Graduation Outcomes:** `graduation.csv` - Graduation rates and outcomes.
6.  **Demographics:** `demographics.csv` - Demographic information for each school.
7.  **Surveys:** `survey_all.txt` & `survey_d75.txt` - Surveys of parents, teachers, and students.

---

### Technology Stack

* **Language:** Python 3.x
* **Libraries:**
    * `pandas` for data manipulation and analysis.
    * `numpy` for numerical operations.
    * `re` (Regular Expressions) for string parsing.
    * `matplotlib` for data visualization.

---

### Methodology

The project followed a structured data analysis process:

1.  **Data Ingestion & Unification:** Read in all seven datasets. A unique school identifier, the District Borough Number (`DBN`), was created for each dataset to serve as a primary key for merging. This involved string padding and concatenation for some files.

2.  **Data Cleaning & Preprocessing:**
    * Converted relevant columns to numeric types, coercing errors where necessary.
    * Extracted latitude and longitude from a combined location string using regular expressions.
    * Filtered datasets to include only relevant data (e.g., grades "09-12" for class size, "2006" cohort for graduation).
    * Aggregated data to the school level (`DBN`) using the mean for datasets like `class_size`.
    * Handled missing values by filling them with the column mean for numerical data and `0` for categorical data after all merges were complete.

3.  **Feature Engineering:**
    * Created a `sat_score` column by summing the three individual SAT section scores.
    * Calculated the percentage of students who took AP exams (`ap_per`) for each school.

4.  **Exploratory Data Analysis (EDA):**
    * Calculated the correlation matrix between `sat_score` and all other numeric columns.
    * Created bar charts and scatter plots to visualize the relationships between SAT scores and key variables, including:
        * Survey responses (safety, academic standards).
        * Demographic percentages (race and gender).
        * AP exam participation.

---

### Key Findings & Insights

* **Safety and Academic Standards:** There is a positive correlation between SAT scores and how students/teachers perceive school safety (`saf_s_11`, `saf_t_11`). Interestingly, student perception of academic standards (`aca_s_11`) correlates with SAT scores, while teacher and parent perceptions do not show a similar trend.

* **Racial Demographics:** A higher percentage of White or Asian students at a school correlates positively with SAT scores. Conversely, a higher percentage of Black or Hispanic students correlates negatively. Further investigation revealed that many schools with a high percentage of Hispanic students primarily serve recent immigrants, suggesting that English language proficiency is a significant underlying factor.

* **Gender:** A higher percentage of female students correlates positively with SAT scores, while a higher percentage of male students correlates negatively. However, the correlation is not very strong. Schools with a high percentage of female students and high SAT scores tend to be selective liberal arts schools.

* **AP Exam Participation:** There is a clear, though not extremely strong, positive correlation between the percentage of students taking AP exams and the school's average SAT score. This suggests that schools with a strong academic focus and college preparation culture tend to perform better overall.
