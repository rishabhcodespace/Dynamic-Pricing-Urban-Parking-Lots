# 🚗 Dynamic Pricing for Urban Parking Lots

**Capstone Project | Summer Analytics 2025**  
Hosted by [Consulting & Analytics Club, IIT Guwahati](https://www.caciitg.com/) × [Pathway](https://pathway.com)

---

## 📌 Project Overview

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

## 🧰 Tech Stack

| Tool/Library | Purpose |
|--------------|---------|
| **Python** (NumPy, Pandas) | Data processing and demand modeling |
| **Pathway** | Real-time data ingestion, processing, and streaming |
| **Bokeh** + **Panel** | Interactive price visualizations |
| **Google Colab** | Development environment |
| **CSV** | Historical parking data (73 days, 14 lots) |

---

## 🏗️ Architecture Diagram (Mermaid)

You can copy this to [Mermaid Live Editor](https://mermaid.live/edit) to render it.

```mermaid
graph TD
    A[CSV: Historical Parking Data] -->|Streamed| B(Pathway replay_csv)
    B --> C{Process Features}
    C --> D1[Model 1: Linear Pricing]
    C --> D2[Model 2: Demand-Based Pricing]
    D2 --> E[Price Predictions (per lot per day)]
    E --> F[Bokeh + Panel Dashboard]

🔍 Project Architecture & Workflow
1. Data Ingestion
The raw dataset (parking_stream.csv) contains real-time snapshots of 14 parking lots across 73 days.

Each snapshot includes features like timestamp, occupancy, queue length, traffic level, special day flags, and vehicle type.

Pathway's replay_csv() was used to simulate real-time streaming of this data.

2. Model 1: Baseline Linear Pricing
A simple reference model:

Copy
Edit
Price_t+1 = Price_t + α × (Occupancy / Capacity)
Price increases linearly as occupancy increases.

Used to benchmark improvements in Model 2.

3. Model 2: Demand-Based Pricing
A weighted model using 5 key demand indicators:

python
Copy
Edit
Demand = α·(Occupancy/Capacity) + β·QueueLength − γ·Traffic + δ·IsSpecialDay + ε·VehicleTypeWeight
Price = BasePrice · (1 + λ · NormalizedDemand)
Weights were hand-tuned and interpreted.

Demand was normalized and price was bounded between 0.5× and 2× base price.

Implemented entirely using Pathway.with_columns() and pw.apply() logic.

4. Real-Time Visualization
A live dashboard was built using Bokeh and Panel.

Users can:

Select a parking lot from a dropdown.

See a time-series plot of real-time pricing.

Each day's price is computed using tumbling windows.
