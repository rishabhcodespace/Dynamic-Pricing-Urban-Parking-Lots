#  Dynamic Pricing for Urban Parking Lots

**Capstone Project | Summer Analytics 2025**  
Hosted by [Consulting & Analytics Club, IIT Guwahati](https://www.caciitg.com/) × [Pathway](https://pathway.com)

---

##  Project Overview

Urban parking spaces are a scarce and valuable resource, especially in cities. Static pricing often leads to inefficiencies: either overcrowding (when prices are too low) or underutilization (when prices are too high).  

This project aims to build an **intelligent, real-time pricing engine** for urban parking lots. The system adjusts prices dynamically based on real-time demand factors like:

- Parking occupancy
- Queue length
- Traffic congestion
- Special days (e.g., events, holidays)
- Vehicle type (car, bike, truck)

Two pricing models were implemented:
- **Model 1**: A baseline linear pricing model
- **Model 2**: A more advanced, demand-based pricing model using a weighted formula

Real-time streaming was simulated using **Pathway**, and interactive price visualizations were built with **Bokeh + Panel**.

---

##  Tech Stack

| Tool/Library | Purpose |
|--------------|---------|
| **Python** (NumPy, Pandas) | Data processing and demand modeling |
| **Pathway** | Real-time data ingestion, processing, and streaming |
| **Bokeh** + **Panel** | Interactive price visualizations |
| **Google Colab** | Development environment |
| **CSV** | Historical parking data (73 days, 14 lots) |

---

##  Architecture Diagram (Mermaid)

![image](https://github.com/user-attachments/assets/f212536e-f55e-458b-9577-449594110b29)

---
##  Project Architecture & Workflow

###  **Data Ingestion**
- The raw dataset (`parking_stream.csv`) contains real-time snapshots of **14 parking lots** over **73 days**.
- Each snapshot includes features like:
  - `timestamp`
  - `occupancy`
  - `queue length`
  - `traffic level`
  - `special day flags`
  - `vehicle type`
- Pathway’s `replay_csv()` was used to simulate **real-time streaming** of this data into a processing pipeline.

## Model 1: Baseline Linear Pricing
A simple reference model for dynamic pricing:

- Price_t+1 = Price_t + α × (Occupancy / Capacity)
- Select a parking lot from a dropdown.
- See a time-series plot of real-time pricing.
- Each day's price is computed using tumbling windows.

## Model 2: Demand-Based Pricing
- Demand = α·(Occupancy / Capacity) + β·QueueLength − γ·Traffic + δ·IsSpecialDay + ε·VehicleTypeWeight
- Price = BasePrice · (1 + λ · NormalizedDemand)
- All weights (α, β, γ, δ, ε, λ) were manually tuned and interpreted.
- Demand normalization ensures stable pricing
- Prices are clipped between 0.5× and 2× the base price.
- Entire logic implemented using Pathway.with_columns() and pw.apply().

## Real-Time Visualization
A live interactive dashboard was built using Bokeh and Panel.

Features : 
- Dropdown to select a parking lot.
- Real-time line chart showing pricing fluctuations.
- Prices are computed using tumbling daily windows over the stream.

## Assumptions
  - IsSpecialDay is binary:
  - 0 = normal, 1 = holiday or event
  - VehicleTypeWeight mapping:
  - car = 1.0
  - bike/cycle = 0.5
  - truck = 1.5
  - TrafficLevel mapping:
  - low = 0.2, average = 0.5, high = 1.0
  - QueueLength capped at 5 for normalization purposes

## Future Work
- Implement Model 3: Competitive Pricing using lat-long proximity
- Add rerouting suggestions for full parking lots
- Optimize demand weights using historical revenue or occupancy patterns

##  Installation & Setup

All code runs in Google Colab, so no setup is required.
If you want to run locally, follow the steps below.

### **1. Clone the repository**
```
git clone https://github.com/your-username/urban-parking-dynamic-pricing.git
cd urban-parking-dynamic-pricing
```

### **2. Install dependencies**

pip install pandas numpy bokeh panel pathway

## How to Run the Project ? 
### **Option 1: Run in Google Colab (recommended)**
- Open notebook.ipynb in Google Colab.
- Follow step-by-step:
 - `Data Preprocessing`
 - `Model 1 and Model 2 implementation`
 - `Real-time streaming with Pathway`
 - `Live Bokeh dashboard via Panel`

- At the end, run:
 - **pw.run()**

### **Option 2: Run locally in Jupyter Notebook**
- Launch Jupyter Notebook:
   - **jupyter notebook**

- Open notebook.ipynb
- Run each cell in order
- Make sure Panel extensions load correctly:
  - **pn.extension()**
    
---
👤 Author
- Rishabh Kumar
- Summer Analytics 2025 Participant
- Consulting & Analytics Club × Pathway
