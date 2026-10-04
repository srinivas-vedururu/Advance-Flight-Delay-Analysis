# ✈️ Advanced Flight Delay Analysis using Python

### *A Production-Grade Exploratory Data Analysis & Statistical Investigation of 336,776 NYC Flights*

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python\&logoColor=white)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter\&logoColor=white)](flight_delay_analysis_pro.ipynb)
[![Executive Insights](https://img.shields.io/badge/Executive%20Insights-Briefing%20Doc-7C3AED?logo=readme\&logoColor=white)](INSIGHTS.md)
[![Plotly](https://img.shields.io/badge/Plotly-Interactive%20Charts-3F4F75?logo=plotly\&logoColor=white)](https://plotly.com)
[![SciPy](https://img.shields.io/badge/SciPy-Hypothesis%20Testing-8CAAE6?logo=scipy\&logoColor=white)](https://scipy.org)
[![Status](https://img.shields.io/badge/Project%20Status-Complete%20%26%20Pre--Rendered-10B981)](#)

> 📖 **Deep Dive Document:** For the complete, uncompressed analytical report with detailed carrier tables, hourly progression metrics, and route rankings, see the [**Full Empirical Insights Briefing (INSIGHTS.md)**](INSIGHTS.md).

---

## 📓 Two Notebook Versions

This project includes **two Jupyter notebooks** for different levels of analysis:

| Notebook     | Description                                                                                                                                                                                                              |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 📘 **Basic** | `flight_delay_analysis_basic.ipynb` — Clean, focused EDA covering data preparation, descriptive statistics, core trends, and essential visualizations.                                                                   |
| 🚀 **Pro**   | `flight_delay_analysis_pro.ipynb` — Advanced analysis with statistical hypothesis testing, interactive visualizations, carrier and airport comparisons, temporal analysis, route insights, and business recommendations. |

**👉 Start with the Basic notebook for a quick overview, or explore the Pro notebook for the complete analytical investigation.**

---

## 📌 Executive Summary

Flight delays create significant operational, financial, and customer-experience challenges across the aviation industry. This project delivers an end-to-end analysis of **336,776 commercial flights** departing from the New York metropolitan area — **JFK, LGA, and EWR** — during 2013.

The analysis goes beyond standard summary statistics to investigate **delay propagation, carrier reliability, airport performance, temporal patterns, route behavior, and statistical significance** across multiple operational dimensions.

---

## 🎯 Key Metrics & High-Level KPIs

| Metric                       |    Value   | Business Context                                         |
| :--------------------------- | :--------: | :------------------------------------------------------- |
| **Total Analyzed Flights**   |  `336,776` | Complete 2013 dataset across 3 NYC airports              |
| **FAA On-Time Performance**  |   `71.6%`  | Flights departing within 15 minutes of schedule          |
| **System Delay Rate**        |   `28.4%`  | Flights with departure delay > 15 minutes                |
| **Average Departure Delay**  | `12.6 min` | Mean departure delay                                     |
| **Median Departure Delay**   | `-2.0 min` | More than half of flights departed early                 |
| **Cancellation Rate**        |   `2.45%`  | 8,255 cancelled flights                                  |
| **Delay Predictability (r)** |   `0.937`  | Strong relationship between departure and arrival delays |

---

## 🔍 Core Analytical Discoveries

### 1. The "Snowball" Ripple Effect

* **Morning Golden Hour (05:00–08:00):** Delay rates remain low at approximately **8.2%**, with average departure delays below **2 minutes**.
* **Evening Gridlock (17:00–20:00):** Delay rates rise to approximately **48.7%**, with average delays exceeding **25 minutes**.
* **Key Insight:** Delays can cascade throughout the day as aircraft turnaround buffers become progressively compressed.

### 2. Hub Bottleneck Comparison

* **Newark Liberty (EWR):** Highest delay rate at approximately **31.2%** and highest mean departure delay at **15.1 minutes**.
* **LaGuardia (LGA):** Lowest mean delay at approximately **10.3 minutes**.
* **JFK:** Moderate delay rate at approximately **27.4%**, with longer ground-transit patterns contributing to operational delays.

### 3. Airline Reliability

* **Top Performers:** Hawaiian Airlines (HA) and Alaska Airlines (AS) achieved on-time rates above **84%**.
* **Higher Delay Rates:** ExpressJet (EV) and Frontier (F9) recorded delay rates above **38%**.

### 4. Seasonality & Weather Patterns

* **Peak Delay Months:** June, July, and December.
* **Calmer Period:** September through November generally showed lower delay rates.
* **Operational Factors:** Weather conditions, holiday demand, airspace congestion, and turnaround constraints contribute to seasonal variation.

---

## 🧪 Statistical Hypothesis Testing

The Pro notebook validates observed patterns using formal statistical tests.

```python
# 1. Airport Delay Homogeneity
# Kruskal-Wallis H-Test
# H0: Delay distributions are identical across EWR, JFK, and LGA
# Result: H = 1,234.82, p < 1e-250
# Decision: Reject H0

# 2. Weekday vs. Weekend Operational Divergence
# Mann-Whitney U Test
# H0: Weekday delays equal weekend delays
# Result: U = 1.28e10, p < 1e-45
# Decision: Reject H0

# 3. Seasonal Delay Variation
# Kruskal-Wallis H-Test
# H0: Delay distributions do not vary across seasons
# Result: H = 3,418.15, p < 1e-300
# Decision: Reject H0

# 4. Departure vs. Arrival Delay
# Pearson Correlation
# Pearson r = 0.937, p < 1e-300
# Takeaway: Departure delays strongly carry through to arrival.
```

---

## 📊 Visualizations Included

The Pro notebook includes **12+ custom interactive visualizations**, including:

1. **Executive KPI Dashboard** — Six-panel management overview.
2. **Delay Distribution** — Histogram and delay-category breakdown.
3. **Correlation Analysis** — Departure vs. arrival delay with regression trendline.
4. **Airport Violin Plots** — Delay distribution comparison across EWR, JFK, and LGA.
5. **Hourly Delay Trends** — Delay probability and average delay by hour.
6. **Day × Hour Heatmap** — Weekly congestion hotspots.
7. **Airline Performance Quadrant** — Flight volume, delay rate, and performance comparison.
8. **Origin-Destination Treemap** — Major routes weighted by flight volume and delay severity.
9. **Interactive Sunburst** — Airport → Airline → Delay Severity hierarchy.

---

## 💡 Strategic Business Recommendations

### 🛫 Airline Operations

* **Dynamic Turnaround Buffering:** Increase turnaround buffers during high-risk afternoon and evening operating windows.
* **EWR Schedule Optimization:** Reduce peak departure concentration during high-congestion periods.
* **Delay Prediction:** Provide customers with estimated on-time probabilities during booking and pre-departure workflows.

### 🧳 Traveler Recommendations

* **Early Departures:** Flights departing before **09:00 AM** generally have substantially lower delay risk.
* **Airport Selection:** Consider airport-specific delay patterns when choosing between NYC gateways.
* **High-Risk Windows:** Exercise additional caution with late-afternoon and evening departures during high-delay months.

---

## 🛠️ Tech Stack

* **Language:** Python 3.12
* **Data Manipulation:** pandas 2.2+, NumPy
* **Visualization:** Plotly 7.1+, Seaborn
* **Statistical Analysis:** SciPy
* **Statistical Tests:** Kruskal-Wallis, Mann-Whitney U, Pearson correlation
* **Environment:** Jupyter Notebook
* **Presentation:** HTML/CSS, interactive Plotly visualizations

---

## 📁 Project Structure

```text
.
├── flight_delay_analysis_basic.ipynb
├── flight_delay_analysis_pro.ipynb
├── flight_delay_intelligence_report.html
├── INSIGHTS.md
└── README.md
```

---

## 🚀 How to Run or View

### 1. 📘 Basic Notebook

Open [`flight_delay_analysis_basic.ipynb`](flight_delay_analysis_basic.ipynb) in VS Code, JupyterLab, or GitHub for the streamlined EDA and core findings.

### 2. 🚀 Pro Notebook

Open [`flight_delay_analysis_pro.ipynb`](flight_delay_analysis_pro.ipynb) for the complete advanced analysis, including statistical testing, interactive visualizations, and business insights.

### 3. 🌐 Interactive Web Report

Open [`flight_delay_intelligence_report.html`](flight_delay_intelligence_report.html) in any modern web browser to explore the standalone interactive report.

### 4. 🔄 Re-run the Analysis

Install the required dependencies:

```bash
pip install pandas numpy plotly scipy seaborn
```

Run the Basic notebook:

```bash
jupyter notebook flight_delay_analysis_basic.ipynb
```

Or run the Pro notebook:

```bash
jupyter notebook flight_delay_analysis_pro.ipynb
```

---

## 📈 Project Scope

The project investigates flight-delay behavior across multiple dimensions:

* Airport performance
* Airline reliability
* Departure time
* Day of week
* Seasonality
* Departure vs. arrival delays
* Cancellation patterns
* Route-level performance
* Delay severity
* Statistical significance
* Operational recommendations

---

<div align="center">

## ✈️ Thank You for Exploring This Project!

### Vedururu Srinivasa Rao : )

</div>
