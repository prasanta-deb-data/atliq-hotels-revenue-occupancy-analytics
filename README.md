# 🏨 AtliQ Hotels Revenue & Occupancy Analytics

> End-to-end hotel analytics project using Python and Pandas to analyze revenue, occupancy, booking channels, cancellations, customer ratings, and property performance.

## 📌 Project Overview

AtliQ Hotels operates properties across multiple cities and needs a data-driven view of hotel performance.

This project analyzes booking-level and aggregated hotel data to answer business questions around:

- Revenue performance
- Occupancy
- Property performance
- Room-class demand
- Booking platforms
- Cancellation behavior
- Revenue leakage
- Customer ratings
- City-level performance

The analysis transforms raw hotel data into business-focused KPIs, performance comparisons, and actionable recommendations.

---

## 🎯 Business Problem

Hotel management needs to understand:

1. Which cities and properties generate the highest realized revenue?
2. Which properties and room classes have the strongest occupancy?
3. How does occupancy differ between weekdays and weekends?
4. Which booking platforms contribute the most revenue?
5. Where are cancellation rates and revenue leakage highest?
6. Which properties require attention or further investigation?
7. What business actions can be considered based on the observed patterns?

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Python | Data analysis and transformation |
| Pandas | Data cleaning, joins and aggregation |
| NumPy | Numerical calculations |
| Matplotlib | Data visualization |
| Jupyter Notebook | Analysis and documentation |
| Git | Version control |
| GitHub | Portfolio and project sharing |

---

## 📂 Project Structure

```text
atliq-hotels-revenue-occupancy-analytics/
│
├── data/
│   ├── raw/
│   │   └── Source datasets
│   │
│   └── processed/
│       └── Processed datasets
│
├── notebooks/
│   └── AtliQ_Hotels_Portfolio_Analysis.ipynb
│
├── outputs/
│   ├── figures/
│   └── reports/
│
├── src/
│   └── README.md
│
├── .gitignore
├── requirements.txt
└── README.md
```

> Raw CSV datasets are intentionally excluded from GitHub through `.gitignore`.

---

## 📊 Data Sources

| Dataset | Description |
|---|---|
| `dim_date.csv` | Calendar and date attributes |
| `dim_hotels.csv` | Hotel/property information |
| `dim_rooms.csv` | Room category and room-class information |
| `fact_bookings.csv` | Booking-level transactional data |
| `fact_aggregated_bookings.csv` | Aggregated booking and capacity data |
| `new_data_august.csv` | Incremental August booking data |

### Analytical Model

```text
                    dim_date
                       │
                       │
dim_rooms ── fact_aggregated_bookings ── dim_hotels


                    dim_date
                       │
                       │
                  fact_bookings
                       │
                       │
                   dim_hotels
```

---

# 🔎 Analysis Approach

## 1. Data Loading

All source datasets are loaded using Pandas.

The notebook uses a repository-aware path structure so the analysis can be reproduced using:

```text
data/raw/
```

rather than relying on a local `datasets/` folder.

## 2. Data Quality Assessment

The analysis checks:

- Missing values
- Duplicate records
- Invalid guest counts
- Revenue outliers
- Missing capacity
- Bookings exceeding capacity
- Invalid dates

## 3. Data Cleaning

The project applies explicit cleaning rules.

### Invalid Guest Records

Records where:

```text
no_guests <= 0
```

are treated as invalid.

### Revenue Outliers

Extreme `revenue_generated` observations are reviewed using:

```text
Mean + 3 × Standard Deviation
```

### Capacity Validation

Records where:

```text
successful_bookings > capacity
```

are treated as invalid occupancy observations.

### Date Handling

Dates are parsed explicitly using day-first interpretation to avoid ambiguous date conversion.

---

# 📈 Key KPIs

The notebook calculates:

- Total bookings
- Cancelled bookings
- No-show bookings
- Cancellation rate
- No-show rate
- Revenue generated
- Revenue realized
- Revenue loss
- Revenue realization rate
- Overall occupancy
- Average customer rating

### Revenue Loss Definition

```text
Revenue Loss =
Revenue Generated − Revenue Realized
```

This is treated as a dataset-specific revenue gap rather than assuming that every difference represents cancellation loss.

---

# 📊 Analysis Performed

## Occupancy Analysis

Occupancy is analyzed across:

- Cities
- Properties
- Room classes
- Weekdays vs weekends
- Months

## Revenue Analysis

Revenue analysis includes:

- Revenue by city
- Revenue by property
- Monthly revenue trend
- Generated vs realized revenue
- Revenue leakage

## Booking Platform Analysis

Booking channels are compared using:

- Booking volume
- Realized revenue
- Average revenue per booking
- Cancellation rate
- Customer rating

## Customer Experience

Customer ratings are analyzed by:

- City
- Property
- Booking platform

Missing ratings are not artificially imputed.

---

# 🏨 Property Performance Segmentation

Properties are classified using median revenue and occupancy thresholds.

### Protect & Scale

High revenue + high occupancy.

### Pricing / Revenue Opportunity

High occupancy + below-median revenue.

### Demand / Conversion Opportunity

High revenue + below-median occupancy.

### Turnaround Candidate

Below-median revenue + below-median occupancy.

These categories are intended as management screening tools, not predictive models.

---

# 💡 Business Insights

The completed notebook generates data-driven insights covering:

### Revenue Leadership

Identifies the city and properties contributing the highest realized revenue.

### Occupancy Leadership

Identifies cities and room classes with the strongest occupancy.

### Demand Timing

Compares weekday and weekend occupancy patterns.

### Booking Channel Performance

Highlights platforms contributing the most realized revenue and compares cancellation behavior.

### Property Opportunities

Uses revenue and occupancy together to identify properties that may require:

- Pricing review
- Demand-generation initiatives
- Conversion improvements
- Performance protection
- Turnaround investigation

---

# 💼 Business Recommendations

### 1. Strengthen Weekday Demand

If weekend occupancy is materially higher than weekday occupancy, investigate:

- Corporate packages
- Weekday promotions
- Differentiated pricing
- Local corporate partnerships

### 2. Protect High-Performing Properties

High-revenue and high-occupancy properties should be monitored for:

- Capacity constraints
- Lost demand
- Pricing opportunities
- Service-quality consistency

### 3. Review High-Cancellation Channels

Channels with elevated cancellation rates should be investigated through:

- Cancellation policies
- Booking lead time
- Discounting
- Customer mix
- Channel economics

### 4. Prioritize Underperforming Properties

Low-revenue and low-occupancy properties can be investigated by:

- City
- Room class
- Booking platform
- Customer rating
- Booking status

### 5. Connect Customer Experience with Commercial Performance

Properties with strong revenue but relatively weaker ratings may require service-quality investigation.

> These recommendations are analytical hypotheses. Additional pricing, inventory, customer-segment and cost data would be required to validate the underlying causes.

---

# 📓 Notebook

The complete analysis is available here:

[`notebooks/AtliQ_Hotels_Portfolio_Analysis.ipynb`](notebooks/AtliQ_Hotels_Portfolio_Analysis.ipynb)

The notebook contains the complete workflow:

```text
Data Loading
      ↓
Data Quality
      ↓
Cleaning
      ↓
Transformation
      ↓
KPI Development
      ↓
Exploratory Analysis
      ↓
Performance Segmentation
      ↓
Business Insights
      ↓
Recommendations
```

---

# 🚀 How to Run the Project

## 1. Clone the repository

```bash
git clone https://github.com/prasanta-deb-data/atliq-hotels-revenue-occupancy-analytics.git
```

## 2. Navigate into the project

```bash
cd atliq-hotels-revenue-occupancy-analytics
```

## 3. Create a virtual environment

Windows:

```bash
python -m venv .venv
```

Activate it:

```bash
.venv\Scripts\activate
```

## 4. Install dependencies

```bash
pip install -r requirements.txt
```

## 5. Add the source datasets

Place the supplied CSV files inside:

```text
data/raw/
```

The raw files are intentionally excluded from GitHub.

## 6. Launch Jupyter

```bash
jupyter notebook
```

Open:

```text
notebooks/AtliQ_Hotels_Portfolio_Analysis.ipynb
```

Then run:

```text
Kernel → Restart & Run All
```

---

# ⚠️ Data Availability

The raw CSV files are not included in the GitHub repository.

They are excluded using:

```gitignore
data/raw/*.csv
data/processed/*.csv
```

This keeps the repository lightweight and avoids redistributing source data without confirming its redistribution rights.

---

# 📌 Portfolio Highlights

This project demonstrates practical Data Analyst capabilities.

### Data Analytics

- Data cleaning
- Data validation
- Exploratory Data Analysis
- KPI development
- Aggregation
- Data transformation

### Business Analytics

- Revenue analysis
- Occupancy analysis
- Property benchmarking
- Booking-channel analysis
- Cancellation analysis
- Customer experience analysis
- Business recommendations

### Technical Skills

```text
Python
Pandas
NumPy
Matplotlib
Jupyter
Git
GitHub
```

---

# 👤 Author

**Prasanta Kumar Deb**

Data Analyst | Python | SQL | Power BI | Data Analytics

---

## ⭐ Project

If you find this project useful, feel free to explore the notebook and analysis.
