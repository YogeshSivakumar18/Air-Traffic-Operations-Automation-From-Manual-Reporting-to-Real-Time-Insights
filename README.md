# Air-Traffic-Operations-Automation-From-Manual-Reporting-to-Real-Time-Insights

## 🚩 Problem Statement

Every day, multiple airspace sectors record data on flights handled, delays, and disruption causes (weather or technical).  

At the end of the day, supervisors **collect all this data manually in Excel** to answer questions like:
- Which sectors were overloaded?  
- How many flights were delayed?  
- Were there enough controllers on duty?

It’s a **slow, repetitive, and error-prone process** that delays crucial operational decisions.

This approach leads to:
- ⏱️ **Delayed situational awareness** – reports are compiled hours after operations  
- 👥 **Inefficient staffing decisions** – no real-time workload visibility  
- 📉 **Lack of performance insight** – data isn’t structured for analysis or automation  

---

## ⚙️ The Workflow Solution


## **Retrieves daily ATC sector reports from Gmail → processes and stores data in the database automatically → serves real-time KPIs through an n8n API for live monitoring.**

### 📨 Step 1: The Data Arrives
Every morning, new **ATC flight reports** are sent by email as CSV attachments.  
Instead of downloading them manually, **n8n’s Gmail trigger** automatically detects and fetches these emails as soon as they arrive.

---

### 🧾 Step 2: The Data is Organized
Once the email is received:
1. **n8n** extracts the attached CSV file.  
2. It parses the flight data — flights handled, delays, weather and tech issues, controller count, etc.  
3. The clean, structured data is stored securely in a **Supabase PostgreSQL database**.

This replaces messy Excel files with an organized, queryable dataset.

---

### 🧮 Step 3: The Data is Transformed
Inside Supabase, a **SQL view** (`atc_kpi_dashboard`) automatically calculates:
- Total flights handled per day  
- Average delay time  
- Weather and technical disruptions  
- Flights per controller  
- % of sectors with high workload  

So instead of hundreds of rows, supervisors see clear **daily KPIs** — one row per day.

---

### 🌐 Step 4: The Data Becomes an API
An **n8n Webhook** converts these KPIs into a real-time API endpoint.  
Anyone can fetch the day’s analytics instantly using a URL.

---

## 📊 Key Performance Indicators (KPIs)

| KPI | Description |
|-----|-------------|
| **Total Flights** | Total flights handled across all sectors |
| **Avg Delay (min)** | Mean delay per flight |
| **Weather / Tech Events** | Number of disruptions by cause |
| **Flights per Controller** | Workload efficiency metric |
| **High Workload %** | % of sectors reporting HIGH load |
| **Peak Hour (UTC)** | Hour of maximum operational activity |

---

## 🧠 Tech Stack

| Layer | Tools & Technologies |
|-------|----------------------|
| **Automation** | n8n Cloud |
| **Database** | Supabase (PostgreSQL) |
| **Data Modeling** | SQL Views (`atc_kpi_dashboard`) |
| **Data Source** | Daily ATC sector CSV files (simulated dataset) |
