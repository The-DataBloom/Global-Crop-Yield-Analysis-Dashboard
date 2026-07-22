# 🌾 Global Crop Yield Analysis Dashboard (1990–2013)

<p align="center">

![Power BI](https://img.shields.io/badge/Power_BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Measures-blue)
![Power Query](https://img.shields.io/badge/Power_Query-ETL-green)

</p>

> **Data Bloom 🌸**  
> Exploring Global Agricultural Productivity Through Interactive Power BI Analytics

<p align="center">
  <img src="Output/preview.png" alt="Global Crop Yield Analysis Dashboard" width="950">
</p>

---

## 📖 Project Story

Sometimes the best projects begin with simple curiosity.

While exploring datasets on **Kaggle**, I discovered a dataset about global crop yields. At first glance, it looked like a typical agricultural dataset, but after exploring its variables—crop yield, rainfall, temperature, pesticides, countries, and years—I realized it could tell a much richer story.

As someone interested in nature, botany, and environmental topics, I transformed this raw dataset into an interactive **Power BI dashboard** capable of answering meaningful questions about agricultural productivity around the world.

This project was developed as part of **Data Bloom 🌸**, where the goal is to transform raw data into clean, interactive, and insight-driven dashboards.

---

## 📑 Table of Contents

- [Project Objective](#-project-objective)
- [Dataset](#-dataset)
- [Data Preparation](#-data-preparation)
- [Data Modeling & DAX](#-data-modeling--dax-measures)
- [Dashboard Overview](#-dashboard-overview)
- [Key Insights](#-key-insights)
- [Design](#-dashboard-design--color-palette)
- [Tools Used](#-tools-used)
- [Repository Structure](#-repository-structure)

---

## 🎯 Project Objective

This dashboard provides a high-level overview of global agricultural productivity by answering questions such as:

- 🌍 How has crop yield changed over time?
- 📈 Which countries achieve the highest average yield?
- 🌾 Which crops contribute the most to overall productivity?
- 📊 How has agricultural performance evolved between **1990 and 2013**?

Rather than presenting raw numbers, the dashboard focuses on **visual storytelling** and **interactive exploration**.

---

## 📂 Dataset

The dataset combines agricultural and climate-related information collected from multiple international sources.

**Sources**

- FAO (Food and Agriculture Organization)
- World Bank

### Main Fields

| Column | Description |
|--------|-------------|
| Area | Country |
| Item | Crop Type |
| Year | Observation Year |
| Yield | Crop Yield |
| Rainfall | Average Annual Rainfall |
| Temperature | Average Annual Temperature |
| Pesticides | Pesticide Usage |

---

## 🛠 Data Preparation

The dataset was cleaned and transformed using **Power Query**.

Main preparation steps included:

- Removing unnecessary columns
- Renaming fields
- Correcting data types
- Handling missing values
- Preparing the data model for DAX calculations

---

# 📐 Data Modeling & DAX Measures

To keep the model clean and maintainable, all calculations were created inside a dedicated **Measure Table**.

Benefits of using measures:

- 🚀 Better performance
- 📊 Dynamic calculations
- 🔄 Reusable across visuals
- 🧹 Easier maintenance

---

<details>
<summary><strong>🌾 Core KPI Measures</strong></summary>

### AVG Yield

**Business Question**

> What is the overall agricultural productivity?

```DAX
AVG Yield =
AVERAGE(yield_df[Yield])
```

### Country Count

```DAX
Country Count =
DISTINCTCOUNT(yield_df[Area])
```

### Crop Types

```DAX
Crop Types =
DISTINCTCOUNT(yield_df[Item])
```

### Yield Growth %

```DAX
Yield Growth % =
VAR Yield1990 =
CALCULATE([AVG Yield], yield_df[Year]=1990)

VAR Yield2013 =
CALCULATE([AVG Yield], yield_df[Year]=2013)

RETURN

DIVIDE(
    Yield2013 - Yield1990,
    Yield1990,
    0
)
```

</details>

---

<details>
<summary><strong>⚡ Dynamic Measures</strong></summary>

### Selected Year

```DAX
Selected Year =
VAR MinYear = MIN(yield_df[Year])
VAR MaxYear = MAX(yield_df[Year])

RETURN

IF(
    MinYear = MaxYear,
    FORMAT(MinYear,"0"),
    FORMAT(MinYear,"0") & " - " & FORMAT(MaxYear,"0")
)
```

### Dashboard Title

```DAX
Dashboard Title =
"Global Crop Yield Analysis 🌾 (" &
[Selected Year] &
")"
```

### Dynamic Visual Titles

```DAX
Country Chart Title =
"Top 10 Countries by Average Yield (" &
[Selected Year] &
")"

Crop Chart Title =
"Top 5 Crop Distribution (" &
[Selected Year] &
")"

Line Chart Title =
"Global Yield Trend (" &
[Selected Year] &
")"

Combo Chart Title =
"Crop Rankings Over Time (" &
[Selected Year] &
")"
```

</details>

---

<details>
<summary><strong>🌦 Supporting Measures</strong></summary>

```DAX
AVG Rainfall =
AVERAGE(yield_df[Rainfall])

AVG Temp =
AVERAGE(yield_df[Temperature])

AVG Pesticides =
AVERAGE(yield_df[Pesticides])

Selected Country =
SELECTEDVALUE(yield_df[Area])

Selected Crop =
SELECTEDVALUE(yield_df[Item])
```

</details>

---

# 📈 Dashboard Overview

The dashboard contains:

- 🌾 Average Yield KPI
- 🌍 Country Count KPI
- 🌱 Crop Types KPI
- 📈 Yield Growth KPI
- 📉 Global Yield Trend (Line Chart)
- 🌍 Top 10 Countries by Average Yield (Bar Chart)
- 🥔 Top 5 Crop Distribution (Donut Chart)
- 📊 Crop Rankings Over Time (Combo Chart)

---

# 💡 Key Insights

- 📈 Global crop yield steadily increased between **1990–2013**.
- 🌍 European countries consistently ranked among the highest-yield producers.
- 🌾 A small number of staple crops account for a large portion of overall productivity.
- 🎛 Dynamic filtering enables exploration by country, crop, and year.

---

# 🎨 Dashboard Design & Color Palette

| Element | Color | Hex |
|----------|-------|-----|
| Background | Light Cream | `#F7F7F5` |
| Cards | White | `#FFFFFF` |
| Primary | Forest Green | `#2E5339` |
| Secondary | Olive Green | `#7A9E5A` |
| Text | Dark Slate | `#2B2B2B` |
| Labels | Gray | `#6B6B6B` |
| Negative | Terracotta | `#C1502E` |
| Positive | Leaf Green | `#5B8C51` |

---

# 🚀 Tools Used

- 📊 Power BI Desktop
- 🧹 Power Query
- 🧮 DAX
- 📈 Data Modeling
- 🎨 Dashboard Design

---

# 📁 Repository Structure

```
.
├── Dataset/
├── Project Files/
├── Output/
└── README.md
```

---

## 🌸 Data Bloom

Building clean, interactive, and business-focused data analytics projects with Power BI.

⭐ **If you found this project helpful, consider giving it a star!**
