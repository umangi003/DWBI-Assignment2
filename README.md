# Data Warehousing and Business Intelligence - Assignment 2
### IT23537842 | Devagiri D.M.U.A | Group 1.2 (Y3 S1-WE)

---

## 📋 Assignment Overview

**Module:** IT3021 - Data Warehousing and Business Intelligence  
**Institution:** Sri Lanka Institute of Information Technology (SLIIT)  
**Batch:** Malabe Weekend Batch  
**Year:** 2026  

**Title:** Multidimensional Data Analysis Using OLAP Operations and Power BI on Uber Trips Data

---

## 🗄️ Project Description

This assignment demonstrates a complete Business Intelligence solution built on top of an Uber Trips Data Warehouse. It covers multidimensional cube creation, OLAP operations, and interactive Power BI reporting.

---

## 📁 Repository Structure

```
DWBI-Assignment2/
│
├── 📁 DataWarehouse/
│   └── Uber_Assignment1.bak          # SQL Server Database Backup
│
├── 📁 CubeProject/
│   └── Uber_Trips_SSAS/              # SSAS Visual Studio Solution
│       ├── Data Sources/
│       ├── Data Source Views/
│       ├── Cubes/
│       └── Dimensions/
│
├── 📁 Excel/
│   └── UberTrips_OLAP.xlsx           # Excel OLAP Operations Workbook
│       ├── Roll-Up Sheet
│       ├── Drill-Down Sheet
│       ├── Slice Sheet
│       ├── Dice Sheet
│       └── Pivot Sheet
│
├── 📁 PowerBIReports/
│   └── UberTrips_PowerBI.pbix        # Power BI Report File
│
├── 📁 Document/
│   └── IT23537842_DWBI_Assignment2.pdf  # Full Assignment Report
│
└── README.md
```

---

## 🏗️ Data Warehouse Design

### Schema Type
**Star Schema** — One central fact table connected to six dimension tables.

### Tables

| Table | Type | Description |
|-------|------|-------------|
| Fact_Trip | Fact | Central fact table — one row per trip |
| Dim_Date | Dimension | Date attributes with time hierarchy |
| Dim_Driver | Dimension | Driver profile with SCD Type 2 |
| Dim_Location | Dimension | Trip start and end locations |
| Dim_Rider | Dimension | Rider profile information |
| Dim_Vehicle | Dimension | Vehicle make, model, plate |
| Dim_Weather | Dimension | Weather conditions during trip |

### Key Measures
- `price_usd` — Trip fare in USD
- `distance_kms` — Trip distance in kilometres
- `surge_multiplier` — Price surge factor
- `txn_process_time_hours` — Transaction processing time

---

## 🧊 Step 2: SSAS Cube Implementation

The SSAS cube was built using **Microsoft Visual Studio** with the **Analysis Services Multidimensional Project** template.

### Components Created
- **Data Source:** `DS_UberTrips_DW` — Connected to `Uber_Assignment1` database
- **Data Source View:** `DSV_UberTrips_DW` — All fact and dimension tables
- **Cube:** `Cube_UberTrips` — Fact_Trip as measure group
- **Dimensions:** Dim_Date, Dim_Driver, Dim_Location, Dim_Rider, Dim_Vehicle, Dim_Weather

### Hierarchies
- **Date Hierarchy:** Year → Quarter → Month → Day
- **Location Hierarchy:** Country → City

### Deployment
- Server: `localhost\AS2019`
- Database: `UberTrips_SSAS`

---

## 📊 Step 3: OLAP Operations in Excel

Excel was connected to the SSAS cube via the Data tab using Analysis Services connection (`localhost\AS2019`).

| Operation | Description | Sheet |
|-----------|-------------|-------|
| **Roll-Up** | Summarized trip revenue by Year | Roll-Up |
| **Drill-Down** | Expanded Year → Quarter → Month → Day | Drill-Down |
| **Slice** | Filtered by single City dimension | Slice |
| **Dice** | Filtered by City AND Vehicle Make | Dice |
| **Pivot** | Swapped Year to Columns, City to Rows | Pivot |

---

## 📈 Step 4: Power BI Reports

Power BI Desktop was connected directly to the SQL Server data warehouse (`Uber_Assignment1`).

### DAX Measures Created

```dax
Total Revenue = SUM(Fact_Trip[price_usd])

Total Trips = COUNT(Fact_Trip[trip_key])

Completion Rate % = 
DIVIDE(
    CALCULATE(
        COUNT(Fact_Trip[trip_key]),
        Fact_Trip[trip_status] = "Completed"
    ),
    COUNT(Fact_Trip[trip_key]),
    0
) * 100
```

### Reports

| Report | Description |
|--------|-------------|
| **Report 1** | Matrix visual — City × Vehicle Make × Year with Total Revenue |
| **Report 2** | Cascading slicers (City → Vehicle Make) with bar and pie charts |
| **Report 3** | Drill-down bar chart — Year → Quarter → Month → Day |
| **Report 4** | Drill-through — Summary page to Detail page by City |

### Published to Power BI Service
All reports published to [Power BI Service](https://app.powerbi.com) and verified online.

---

## 🛠️ Tools & Technologies

| Tool | Version | Purpose |
|------|---------|---------|
| SQL Server | 2019 Developer | Data Warehouse hosting |
| SQL Server Management Studio | 22.x | Database management |
| Visual Studio | 2019/2022 | SSAS cube development |
| Microsoft Excel | 2019/365 | OLAP operations |
| Power BI Desktop | Latest | Report development |
| Power BI Service | Online | Report publishing |

---

## ⚙️ Setup Instructions

### 1. Restore Database
```sql
-- In SSMS, restore the backup file
RESTORE DATABASE Uber_Assignment1
FROM DISK = 'path\to\Uber_Assignment1.bak'
```

### 2. Deploy SSAS Cube
- Open `Uber_Trips_SSAS.sln` in Visual Studio
- Update server name in Project Properties → Deployment
- Right click project → Deploy

### 3. Open Excel Workbook
- Open `UberTrips_OLAP.xlsx`
- Refresh connections if prompted
- Each sheet demonstrates one OLAP operation

### 4. Open Power BI Report
- Open `UberTrips_PowerBI.pbix` in Power BI Desktop
- Update data source credentials if prompted
- View all 5 report pages

---

## 👤 Author

**Name:** Devagiri D.M.U.A  
**IT Number:** IT23537842  
**Group:** 1.2 (Y3 S1-WE)  
**Module:** IT3021 - Data Warehousing and Business Intelligence  
**Institution:** SLIIT — Sri Lanka Institute of Information Technology  

---

## 📝 License

This project is submitted as academic work for SLIIT. All rights reserved.
