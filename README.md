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
