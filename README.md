# 🚖 Uber Trip Analysis Dashboard

<p align="center">
  <img src="https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black"/>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white"/>
  <img src="https://img.shields.io/badge/DAX-F2C811?style=for-the-badge&logo=powerbi&logoColor=black"/>
  <img src="https://img.shields.io/badge/Records-103K%2B-black?style=for-the-badge"/>
</p>

<p align="center">
  <b>An end-to-end interactive Power BI dashboard analyzing 103,000+ Uber trips — covering bookings, revenue, time patterns, and location intelligence.</b>
</p>

---

## 📌 Project Overview

This project analyzes real-world Uber trip data from **June 2024** using **Power BI** with advanced DAX measures, dynamic measure selectors, drill-through pages, and heatmap visuals. The goal is to help stakeholders make data-driven decisions on pricing, driver allocation, and demand forecasting.

---

## 📊 Dataset

| File | Description |
|------|-------------|
| `Uber_Trip_Details.xlsx` | 103,728 trip records with fare, distance, vehicle, payment |
| `Location_Table.xlsx` | Location ID to City/Area mapping |

**Key Fields:**
- Trip ID, Pickup Time, Drop-off Time
- Passenger Count, Trip Distance
- Pickup & Drop-off Location IDs
- Fare Amount, Surge Fee
- Vehicle Type *(UberX, UberXL, Uber Black, Uber Comfort, Uber Green)*
- Payment Type *(Uber Pay, Google Pay, Amazon Pay, Cash)*

---

## 📈 Dashboard Pages

### Dashboard 1 — Overview Analysis
> Booking trends, revenue KPIs, vehicle performance, and location hotspots.

**KPIs Tracked:**
- ✅ Total Bookings
- ✅ Total Booking Value
- ✅ Average Booking Value
- ✅ Total Trip Distance
- ✅ Average Trip Distance
- ✅ Average Trip Time

**Visuals:**
- Dynamic Measure Selector (Disconnected Table + DAX Switch)
- Bookings by Payment Type
- Bookings by Trip Type (Day / Night)
- Vehicle Type Grid with Conditional Formatting
- Total Bookings by Day (trend line)
- Top 5 Pickup & Drop-off Locations
- Most Preferred Vehicle per Location

---

### Dashboard 2 — Time Analysis
> Identifying peak hours, busiest days, and demand heatmaps.

**Visuals:**
- Bookings by Pickup Time (10-minute intervals) — Area Chart
- Bookings by Day Name (Mon–Sun) — Line Chart
- Hour × Day Heatmap (Matrix Grid) — highlights peak booking windows

---

### Dashboard 3 — Details Tab
> Granular drill-through data table for deep-dive analysis.

**Features:**
- Full trip-level data grid
- Drill-through from any visual
- "View Full Data" bookmark toggle
- Reset filters button

---

## ⚙️ DAX Measures Used

```dax
-- Dynamic Measure Selector
Selected Measure = 
SWITCH(
    SELECTEDVALUE('Measure Selector'[Measure]),
    "Total Bookings", [Total Bookings],
    "Total Booking Value", [Total Booking Value],
    "Total Trip Distance", [Total Trip Distance],
    [Total Bookings]
)

-- Total Booking Value
Total Booking Value = SUM(uber_trip_details[fare_amount]) + SUM(uber_trip_details[Surge Fee])

-- Average Trip Time (Minutes)
Avg Trip Time = 
AVERAGEX(
    uber_trip_details,
    DATEDIFF(uber_trip_details[Pickup Time], uber_trip_details[Drop Off Time], MINUTE)
)

-- Most Frequent Pickup Location
Top Pickup Location = 
TOPN(1, VALUES(Location[Location]), CALCULATE(COUNTROWS(uber_trip_details)))
```

---

## 🗂️ Data Model

```
Uber_Trip_Details
    ├── PULocationID ──→ Location_Table (LocationID)   [Active]
    └── DOLocationID ──→ Location_Table (LocationID)   [Inactive — activated via USERELATIONSHIP]
```

> Drop-off location analysis uses `USERELATIONSHIP()` in DAX to activate the inactive relationship.

---

## 🔑 Key Insights

- 📍 **Top pickup hotspot:** Identified via location frequency analysis
- 🚗 **Most booked vehicle:** UberX dominates across all locations
- 💳 **Preferred payment:** Uber Pay leads over Cash, Google Pay, Amazon Pay
- 🌙 **Peak hours:** Late evening and early morning show highest surge
- 📅 **Busiest day:** Weekends consistently outperform weekdays in bookings

---

## 🚀 How to Use

1. Clone this repository
   ```bash
   git clone https://github.com/Prathmesh-Sanmukh/Uber_Trip_Analysis_Dashboard.git
   ```
2. Open `uber_analysis.pbix` in **Power BI Desktop**
3. If prompted, re-link the Excel data sources from the `/data` folder
4. Explore all 3 dashboard pages using slicers and drill-through

---

## 🛠️ Tools & Technologies

| Tool | Usage |
|------|-------|
| Power BI Desktop | Dashboard creation, DAX, data modeling |
| DAX | KPI measures, dynamic selector, time intelligence |
| Power Query | Data transformation & cleaning |
| Excel | Raw data source |
| Python (Pandas) | Initial data exploration |

---

## 👤 Author

**Prathmesh Sanmukh**
- 🔗 [LinkedIn](https://www.linkedin.com/in/prathmesh-sanmukh)
- 💻 [GitHub](https://github.com/Prathmesh-Sanmukh)

---

*This project is part of my Data Analyst portfolio showcasing Power BI, DAX, and data storytelling skills.*
