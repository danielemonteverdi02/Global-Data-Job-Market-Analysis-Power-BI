# Global Data Job Market Analysis – Power BI

## 📌 Project Overview

This project analyzes the **global data job market in 2024** using **Power BI**.

The analysis is based on a dataset of approximately **478,000 job postings** collected from Google job search results. The dataset contains information on job roles, companies, locations, salaries, required skills, work arrangements, job schedules, degree requirements, health insurance and job posting platforms.

The main objective of the project is to explore the structure and evolution of the data job market, with a particular focus on:

* job market demand by role and country;
* salary and compensation;
* technical skills required by employers;
* remote work opportunities;
* degree requirements;
* job schedule types;
* temporal trends during 2024;
* the Italian data job market.

The project was developed entirely in **Power BI**, including data modeling, DAX measures, calculated columns, time intelligence and interactive visualizations.

---

## 🎯 Business Questions

The dashboard was designed to answer questions such as:

* How large is the global data job market?
* Which data-related roles have the highest demand?
* Which countries have the largest number of data job postings?
* Which roles have the highest median salaries?
* Which technical skills are most frequently requested?
* How do skill requirements differ across job roles?
* How prevalent are remote positions?
* How frequently do job postings mention degree requirements?
* How does job posting activity change over time?
* Which job platforms are most frequently used?
* What are the main characteristics of the Italian data job market?

---

## 📂 Dataset

The dataset contains job postings collected during **2024** through automated scraping of Google job search results.

The original dataset was collected by the author of Data Nerd and made available in different formats, including:

* `job_postings_flat.csv`

The data used in this project is based on the original **2024 job postings dataset**.

### Main variables

The dataset includes information such as:

| Variable                | Description                                                |
| ----------------------- | ---------------------------------------------------------- |
| `job_title_short`       | Standardized job title                                     |
| `job_title`             | Original job title                                         |
| `job_location`          | Location reported in the job posting                       |
| `job_country`           | Country extracted from the job location                    |
| `job_schedule_type`     | Job schedule type                                          |
| `job_work_from_home`    | Whether the position is remote                             |
| `job_posted_date`       | Job posting date                                           |
| `job_no_degree_mention` | Whether the posting does not mention a degree requirement  |
| `job_health_insurance`  | Whether health insurance is mentioned                      |
| `salary_year_avg`       | Average yearly salary when salary information is available |
| `company_name`          | Company name                                               |
| `job_skills`            | Skills extracted from the job posting                      |
| `job_type_skills`       | Skill categories associated with the posting               |
| `job_via`               | Platform through which the job posting was found           |

---

## ⚠️ Dataset Limitations

The dataset should be interpreted with some limitations in mind.

### Salary information

Salary information is available only for a **small proportion of job postings**. In the dashboard, approximately **4.25% of postings contain salary information**.

Therefore, salary-related statistics such as:

* minimum salary;
* median salary;
* maximum salary;
* salary bands;
* salary comparisons between countries or roles

are calculated only from postings for which a yearly salary value is available.

Furthermore, salary values should **not be interpreted as perfectly standardized international compensation measures**. The dataset does not provide a fully standardized framework for comparing salaries across countries in terms of currency, purchasing power, cost of living or local compensation levels.

Consequently, cross-country salary comparisons should be interpreted with caution.

### Job posting data

The dataset represents **job postings collected through Google job search results**, rather than the complete universe of job vacancies.

The number of postings therefore reflects the data collected by the scraping process and may be affected by:

* search engine coverage;
* source/platform coverage;
* duplicate or repeated postings;
* geographical differences in job posting visibility;
* differences in how job information is reported.

### Skills

Skills were extracted from job postings using automated processing. Therefore, the presence or absence of a skill depends on the information explicitly available in the job posting and the extraction methodology.

A skill not appearing in a posting does not necessarily mean that the employer does not value or use that skill.

---

# 🧱 Data Model

A **star schema** was used to organize the Power BI data model.

The central fact table is:

* `job_postings_fact`

The main dimension tables are:

* `company_dim`
* `skills_dim`
* `skills_job_dim`
* `schedule_dim`
* `Calendar`

The `Calendar` table was created specifically for this project to support time-based analysis and DAX Time Intelligence.

### Main relationships

The model includes relationships between:

* `job_postings_fact` → `company_dim`
* `job_postings_fact` → `skills_job_dim`
* `job_postings_fact` → `Calendar`
* `job_postings_fact` → `schedule_dim`

The model separates job posting information from descriptive dimensions and allows the same job posting data to be analyzed from different perspectives.

---

# 🧹 Data Preparation & Modeling

The project included data preparation and modeling activities in Power BI.

The main steps included:

* importing the job posting data;
* organizing the data according to a star-schema structure;
* creating relationships between fact and dimension tables;
* creating a dedicated Calendar table;
* creating calculated columns for more readable categorical labels;
* creating salary bands;
* creating DAX measures for KPIs and analytical metrics;
* configuring sorting columns for chronological analysis;
* applying conditional formatting to selected visualizations;
* creating interactive slicers and cross-filtering between visuals;
* creating report tooltips containing relevant measures.

---

# 📅 Calendar Table

A dedicated Calendar table was created for the 2024 analysis period.

The table includes:

* Date
* Year
* Month Number
* Month
* Month Short
* Year Month
* Year Month Sort
* Quarter Number
* Quarter
* Year Quarter
* Day
* Day of Week Number
* Day of Week
* Week Number
* Is Weekend

The Calendar table was used to support chronological analysis and DAX Time Intelligence calculations.

A separate `Month End` column was also created using `EOMONTH()` to identify the last day of each month.

---

# 🧮 DAX Measures

A set of explicit DAX measures was created to calculate the main KPIs and analytical metrics.

## Basic aggregation

### Total Jobs

### Total Companies

### Total Skills

### Skill Types

### Average Skills per Job

---

# 💰 Salary Measures

Salary measures were calculated using `salary_year_avg`.

Because salary information is not available for all postings, salary calculations exclude records where the yearly salary value is zero.

### Minimum Salary

### Median Salary

### Maximum Salary

### Jobs With Salary Information

---

# 🏠 Remote Work, Degree & Benefits

Additional measures were created to calculate the proportion of job postings with specific characteristics.

### Remote Jobs

### Degree Mention

### Health Insurance

---

# ⏱️ Time Intelligence

Time Intelligence was implemented using the dedicated `Calendar` table.

### Jobs MTD

### Jobs QTD

### Previous Month Jobs

### Month-over-Month Change

### Previous Quarter Jobs

### Quarter-over-Quarter Change

### Cumulative Jobs

---

# 🏷️ Calculated Columns

Several calculated columns were created to improve the readability and usability of the dashboard.

## Degree Mention Label

Equivalent label columns were also created for:

* Health Insurance
* Work From Home

These columns transform Boolean values into user-friendly categorical labels.

---

# 💵 Salary Band

A categorical salary band was created using `SWITCH()` and `TRUE()`.
This column was used to analyze the distribution of job postings across salary ranges.

---

# 🔧 DAX Functions Used

The main DAX functions used throughout the project include:

### Aggregation functions

* `COUNTROWS()`
* `DISTINCTCOUNT()`
* `MIN()`
* `MAX()`
* `MEDIAN()`

### Filter and context functions

* `CALCULATE()`
* `FILTER()`
* `ALLSELECTED()`
* `DIVIDE()`

### Logical functions

* `IF()`
* `SWITCH()`
* `TRUE()`

### Time Intelligence functions

* `TOTALMTD()`
* `TOTALQTD()`
* `PREVIOUSMONTH()`
* `PREVIOUSQUARTER()`

### Date functions

* `DATE()`
* `YEAR()`
* `MONTH()`
* `DAY()`
* `QUARTER()`
* `WEEKDAY()`
* `WEEKNUM()`
* `EOMONTH()`

### Date formatting functions

* `FORMAT()`

### Calendar generation

* `CALENDAR()`
* `ADDCOLUMNS()`

The project therefore includes both basic DAX aggregation and more advanced **filter-context and Time Intelligence calculations**.

---

# 📊 Dashboard Pages

The report is organized into five analytical sections.

---

## 1. Global Job Market

The first page provides a high-level overview of the global data job market.

### Main KPIs

* Total Jobs
* Total Companies
* Median Salary
* Remote Jobs
* Degree Mention

### Main visualizations

* Monthly Job Postings Trend
* Top Schedule Types
* Health Insurance Coverage
* Global Job Distribution
* Job Market by Role

This page provides a general overview of the size, geographical distribution and main characteristics of the global market.

---

## 2. Salary & Compensation

This page focuses on salary and compensation.

### Main KPIs

* Total Jobs
* Minimum Salary
* Median Salary
* Maximum Salary
* Jobs With Salary Information

### Main visualizations

* Job Market Size vs. Median Salary
* Median Salary by Job Schedule Type
* Country-level salary and job market table
* Job Postings by Salary Band
* Median Salary by Work Arrangement

The scatter plot compares job market size and median salary across different roles, allowing demand and compensation to be analyzed simultaneously.

---

## 3. Skills & Job Profile

This page focuses on the skills requested in data-related job postings.

### Main KPIs

* Total Jobs
* Total Skills
* Average Skills per Job
* Skill Types

### Filters

* Role
* Schedule Type
* Degree Mention

### Main visualizations

* Top 10 Skills by Total Jobs
* Role-level job market matrix
* Top Job Posting Platforms
* Skill Types by Total Jobs
* Skills by Role using a 100% stacked bar chart

The 100% stacked bar chart compares the relative prevalence of the most frequently requested skills across job roles.

For example, it allows the proportion of job postings mentioning skills such as SQL, Python and other frequently requested skills to be compared across different roles.

---

## 4. Time Intelligence

This page focuses on the temporal evolution of job postings during 2024.

### Filters

* Date
* Role
* Country
* Health Insurance
* Degree Mention
* Schedule Type

### Main visualizations

* Cumulative Job Postings by Month
* Job Postings by Quarter
* Job Postings by Day of the Week
* Monthly analytical table

The monthly table includes:

* Year
* Month
* Month End
* Total Jobs
* Jobs MTD
* MoM Change %
* Minimum Salary
* Median Salary
* Maximum Salary
* Remote Jobs

This page demonstrates the use of DAX Time Intelligence functions and a dedicated Calendar table.

---

## 5. Italy Job Market

The final page focuses specifically on the Italian data job market.

### Main KPIs

* Total Jobs
* Total Companies
* Median Salary
* Jobs With Salary Information
* Degree Mention

### Filters

* Role
* Schedule Type
* City

### Main visualizations

* Monthly Job Postings Trend
* Job Market Distribution across Italian locations
* Job Market by Role
* Top 10 Skills
* Top Job Posting Platforms
* Work From Home distribution
* Role-level analytical table

The page allows the global dataset to be analyzed from a specific Italian market perspective.

---

# 🎨 Data Visualization & Interactivity

The dashboard includes several interactive features:

* slicers for dynamic filtering;
* cross-filtering between visualizations;
* conditional formatting;
* KPI cards;
* interactive tables and matrices;
* geographic visualizations;
* custom tooltips;
* multiple analytical pages;
* navigation between report sections.

Tooltips were also used in selected visuals to provide additional information and display relevant measures without overcrowding the main dashboard.

---

# 🔎 Analytical Approach

The project combines descriptive analysis, data modeling and interactive business intelligence.

The analysis moves from a broad overview toward increasingly specific questions:

**Global Job Market**
→ overall market structure

**Salary & Compensation**
→ compensation and job market size

**Skills & Job Profile**
→ employer skill requirements

**Time Intelligence**
→ temporal trends and changes

**Italy Job Market**
→ country-specific analysis

This structure allows the dashboard to be used both as an executive overview and as an exploratory analytical tool.

---

# 🛠️ Tools & Technologies

* **Power BI Desktop**
* **Power Query**
* **DAX**
* **Star Schema Data Modeling**
* **Time Intelligence**
* **Data Visualization**
* **Interactive Dashboard Design**

---

# 📚 Data Source

The original dataset and its documentation are available through the Data Nerd project:

https://datanerd.tech

The dataset was collected from Google job search results using automated scraping.

The data used in this project was not collected personally; the analysis, data model, DAX measures and Power BI dashboard were developed as part of this project.

---

# 🎯 Skills Demonstrated

This project demonstrates practical experience in:

* Power BI dashboard development
* Data modeling
* Star schema design
* Fact and dimension tables
* Data preparation
* DAX measures
* Calculated columns
* Filter context
* Conditional calculations
* Aggregation functions
* Time Intelligence
* Calendar table creation
* MTD and QTD calculations
* MoM and QoQ analysis
* Cumulative calculations
* Salary analysis
* Skills analysis
* Geographic analysis
* Interactive reporting
* Data visualization
* Business-oriented analytical storytelling

---

# 🚀 Possible Future Improvements

Potential extensions of the project could include:

* standardizing salary values across currencies;
* incorporating purchasing-power or cost-of-living adjustments;
* separating salary comparisons by country;
* expanding the analysis to additional years;
* analyzing salary distributions by experience level;
* developing more advanced skill co-occurrence analysis;
* adding year-over-year comparisons once multiple years of data are available;
* incorporating additional geographic and labor-market indicators.

---

## 📌 Project Summary

This project uses Power BI to analyze approximately **478K job postings** and provides an interactive view of the global data job market in 2024.

The project combines **star-schema data modeling, DAX, Time Intelligence, salary analysis, skills analysis, geographic analysis and interactive visualization**, with a dedicated section focused on the Italian job market.
