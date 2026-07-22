# 🌾 Global Crop Yield Analysis Dashboard (1990–2013)

> **Data Bloom 🌸**  
> Exploring Global Agricultural Productivity Through Interactive Power BI Analytics

<p align="center">
  <img src="preview.png" alt="Global Crop Yield Analysis Dashboard" width="950">
</p>

---

# 📖 Project Story

Sometimes the best projects begin with simple curiosity.

While exploring datasets on **Kaggle**, I came across a dataset about global crop yields. At first glance it looked like just another agricultural dataset, but after looking deeper into its variables—crop yield, rainfall, temperature, pesticides, countries, and years—I realized it had the potential to tell a much richer story.

As someone who enjoys nature, botany, and environmental topics, I decided to transform this raw dataset into an interactive Power BI dashboard capable of answering meaningful questions about agricultural productivity around the world.

This project was developed as part of **Data Bloom 🌸**, where the goal is to turn raw data into clean, interactive, and insight-driven dashboards.

---

# 🎯 Project Objective

The purpose of this dashboard is to provide a high-level overview of global agricultural productivity by answering questions such as:

- 🌍 How has crop yield changed over time?
- 📈 Which countries achieve the highest average yield?
- 🌾 Which crops contribute the most to overall productivity?
- 📊 How has agricultural performance evolved between 1990 and 2013?

Rather than presenting raw numbers, the dashboard focuses on visual storytelling and interactive exploration.

---

# 📂 Dataset

The dataset combines agricultural and climate-related information collected from multiple international sources.

It includes data from:

- **FAO** (Food and Agriculture Organization)
- **World Bank**

### Main Fields

| Column | Description |
| :--- | :--- |
| **Area** | Country |
| **Item** | Crop Type |
| **Year** | Observation Year |
| **Yield** | Crop Yield |
| **Rainfall** | Average Annual Rainfall |
| **Temperature** | Average Annual Temperature |
| **Pesticides** | Pesticide Usage |

---

# 🛠 Data Preparation

The dataset was cleaned and transformed using **Power Query** before building the dashboard.

Main preparation steps included:

- Removing unnecessary columns
- Renaming fields for consistency
- Correcting data types
- Handling missing values
- Preparing the data model for DAX calculations

---

# 📐 Data Modeling & DAX Measures

To keep the data model clean and maintainable, all calculations were organized inside a dedicated **Measure Table**.

Using measures instead of calculated columns makes the dashboard:

- 🚀 **More efficient**
- 📊 **Dynamic and filter-aware**
- 🔄 **Reusable across multiple visuals**
- 🧹 **Easier to maintain**

Each measure was designed to answer a specific business question rather than simply performing calculations.

---

## 🌾 AVG Yield

**Business Question**

> *What is the overall agricultural productivity?*

**Purpose**

This measure calculates the average crop yield for the current filter context. Since it is filter-aware, selecting a country, crop, or year instantly updates the KPI and every related visual.

```DAX
AVG Yield =
AVERAGE(yield_df[Yield])

🌍 Country Count
Business Question
> How many countries are currently included in the analysis?
> 
Purpose
Counts the number of distinct countries currently visible after filtering.
This KPI provides users with context about the geographical coverage of the dashboard.
Country Count =
DISTINCTCOUNT(yield_df[Area])

🌱 Crop Types
Business Question
> How many crop categories are being analyzed?
> 
Purpose
Returns the number of unique crop types included in the current selection.
This KPI helps users understand the diversity of agricultural products represented in the dataset.
Crop Types =
DISTINCTCOUNT(yield_df[Item])

📈 Yield Growth %
Business Question
> How much has agricultural productivity changed over time?
> 
Purpose
Compares the average crop yield between 1990 and 2013, providing a high-level indicator of long-term agricultural performance.
Instead of showing two separate values, this measure summarizes historical change into a single KPI.
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

⚡ Dynamic Measures
Besides numerical calculations, several measures were created to improve the dashboard experience by dynamically updating titles and contextual information.

🗓 Selected Year
Purpose
Detects the active year filter and converts it into a readable text format.
Instead of displaying static titles, every chart automatically reflects the selected time period.
Selected Year =
VAR MinYear = MIN(yield_df[Year])
VAR MaxYear = MAX(yield_df[Year])

RETURN

IF(
    MinYear = MaxYear,
    FORMAT(MinYear,"0"),
    FORMAT(MinYear,"0") & " - " & FORMAT(MaxYear,"0")
)

🏷 Dynamic Dashboard Title
Purpose
Automatically updates the dashboard title according to the selected year range, making the report more interactive and reducing ambiguity.
Dashboard Title =
"Global Crop Yield Analysis 🌾 (" &
[Selected Year] &
")"

📊 Dynamic Chart Titles
Purpose
Instead of using fixed titles, every chart updates itself based on the selected filters, ensuring users always understand the context of the displayed data.
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

🌦 Supporting Measures
These measures were created to support future dashboard expansion, advanced tooltips, and additional analytical pages.
Average Rainfall
Provides the average rainfall for the selected filter context.
AVG Rainfall =
AVERAGE(yield_df[Rainfall])

Average Temperature
Calculates the average annual temperature.
AVG Temp =
AVERAGE(yield_df[Temperature])

Average Pesticides
Calculates the average pesticide usage.
AVG Pesticides =
AVERAGE(yield_df[Pesticides])

Selected Country
Returns the currently selected country, making it useful for dynamic titles, cards, or custom tooltips.
Selected Country =
SELECTEDVALUE(yield_df[Area])

Selected Crop
Returns the currently selected crop type. Useful for creating contextual labels and interactive report elements.
Selected Crop =
SELECTEDVALUE(yield_df[Item])

📈 Dashboard Overview
The dashboard is organized into four KPI cards and four main visualizations:

 * 🌾 Average Yield KPI: Provides a dynamic baseline metric for average agricultural productivity.

 * 📈 Global Yield Trend: (Visual: Line Chart) Displays the long-term trend of global average crop yield between 1990 and 2013.

 * 🌍 Top 10 Countries by Average Yield: (Visual: Horizontal Bar Chart) Ranks countries according to their average crop yield.

 * 🥔 Top 5 Crop Distribution: (Visual: Donut Chart) Shows the contribution of the five highest-performing crops.

 * 📊 Crop Rankings Over Time: (Visual: Line & Clustered Column Chart) Combines yearly productivity with crop ranking trends to provide a broader view of agricultural performance over time.

💡 Key Insights
 * Steady Long-Term Growth: Global average crop yield shows an overall upward trend between 1990 and 2013.

 * European Agricultural Dominance: Several European countries consistently appear among the highest-yielding countries in the dataset.

 * High Crop Concentration: A small number of root/staple crops contribute a significant share of the overall average yield volume.

 * Contextual Filtering: Dynamic DAX filters allow seamless exploration across customized year ranges and territories.

🎨 Dashboard Design & Color Palette
The dashboard follows a clean, highly structured, and minimal design inspired by organic agricultural tones.

| Element / Role | Color Description | Hex Code |
|---|---|---|
| Page Background | Off-White / Light Cream | #F7F7F5 |
| Card Background | Pure White | #FFFFFF |
| Primary Brand Color | Deep Forest Green | #2E5339 |
| Secondary Accent | Light Olive Green | #7A9E5A |
| Primary Text | Dark Slate / Almost Black | #2B2B2B |
| Secondary Text / Labels | Medium Neutral Gray | #6B6B6B |
| Negative Growth / Warning | Soft Terracotta / Brick Red | #C1502E |
| Positive Growth Accent | Vibrant Leaf Green | #5B8C51 |

🚀 Tools Used
 * 📊 Power BI Desktop
 * 🧹 Power Query
 * 🧮 DAX
 * 📈 Data Modeling
 * 🎨 Custom Dashboard & Layout Design

📁 Repository Structure
.
├── 📂 Dataset/
├── 📂 Project Files/
├── 📂 Output/
└── 📝 README.md

📸 Dashboard Preview
<p align="center">
<img src="preview.png" alt="Global Crop Yield Dashboard Final Preview" width="1000">
</p>

> Data Bloom 🌸
> Building clean, interactive, and business-focused data analytics projects with Power BI.
> 
⭐ If you enjoyed this project or found it useful, consider giving it a star!

