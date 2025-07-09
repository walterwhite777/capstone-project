# 🚗 Dynamic Pricing for Urban Parking Lots – Summer Analytics 2025

## 📁 Project Overview

This project tackles the challenge of **real-time dynamic pricing** for urban parking spaces using real-time data simulation, Pathway's streaming engine, and Bokeh for live visualization. We aim to dynamically adjust parking prices based on demand, traffic, occupancy, and other external conditions to optimize revenue and usage.

This was completed as part of the **Summer Analytics 2025 capstone project**.

---

## 🧠 Problem Statement

Urban parking lots often follow static pricing, leading to inefficient space utilization. Some lots are overused and congested while others remain empty. Our goal is to implement **smart pricing logic** that:

- Adjusts pricing dynamically in real-time.
- Factors in multiple conditions like occupancy, traffic, special days, and vehicle types.
- Provides visibility to users through live plots using Bokeh.
- Simulates and processes data in real-time using **Pathway's powerful stream processing**.

---

## 🧩 Models Implemented

We designed and implemented the following models:

### ✅ Model 1: Linear Pricing Based on Past Occupancy (Baseline)

- **Logic**: Adjusts price linearly based on the average occupancy in the past 1 day window.
- **Formula**:  
  `price = base_price * (1 + alpha * avg_occupancy)`
- **Windowing**: Tumbling daily window using Pathway.
- **Use Case**: Acts as the baseline for static linear pricing.
- **Visuals**: Bokeh plots showing day-wise price evolution for each parking lot.

---

### ✅ Model 2: Demand-Based Dynamic Pricing (Advanced)

- **Logic**: Calculates a weighted demand score using:
  - Occupancy ratio
  - Queue length
  - Nearby traffic level
  - Whether the day is special (e.g., weekend or event)
  - Type of incoming vehicle
- **Weights Used**:
  - `alpha (Occupancy)`: 0.1  
  - `beta (QueueLength)`: 0.05  
  - `gamma (Traffic)`: 0.02  
  - `delta (SpecialDay)`: 0.02  
  - `epsilon (VehicleWeight)`: 0.03  

- **Final Pricing Formula**:  
  `price = base_price * (1 + λ * normalized_demand)`  
  where λ = 1.5

- **Benefits**:
  - Much more responsive to real-world conditions
  - More stable than Model 1 in volatile traffic zones
  - Greater range of pricing flexibility

- **Visuals**: Real-time dropdown plot for each lot, showing the price curve using Bokeh.

---

## 🔧 Real-Time Simulation Using Pathway

- **Data Ingestion**: Simulated streaming using `replay_csv()` from `Pathway`, mimicking real-time arrival of events.
- **Temporal Logic**: Used `tumbling` and `sliding` windows to aggregate demand over daily intervals.
- **Streaming Behavior**: Uses `exactly_once_behavior()` to maintain correctness during replay.
- **Live Updates**: As data streams in, plots auto-update using Bokeh and Panel widgets.

---

## 📊 Visualizations and Dashboard

All visualizations are created using **Bokeh** and served via **Panel** inside Google Colab:

- **Live line plots for each parking lot** (14 lots total)
- **Interactive dropdown to select lot**
- **Automatic updates as data is replayed**

These make the model’s pricing behavior easy to interpret and justify.

---

## 💡 Assumptions

- Special days are represented as binary (0 or 1), manually extracted from input data.
- OccupancyRatio and TrafficLevel are normalized in `[0, 1]`.
- Missing or unknown vehicle/traffic types are defaulted to average values.
- Data was streamed at a fixed `input_rate` for simulation, although real-world usage would ingest actual feeds.

---

## 📁 Files Included

| File Name                | Description                                      |
|-------------------------|--------------------------------------------------|
| `model1.ipynb`          | Model 1 notebook with linear pricing logic       |
| `model2.ipynb`          | Model 2 notebook with demand-based pricing       |
| `dataset.csv`           | Raw source data                                  |
| `model2_stream.csv`     | Cleaned and preprocessed stream-ready data       |
| `executive_summary.txt` | Report explaining models and pricing logic       |
| `README.md`             | This file with complete project documentation    |
| `demand_model_daily_output.jsonl` | JSONLines output of final pricing data |

---

## 🏁 How to Run (Google Colab Setup)

1. Upload all files to your Colab session.
2. Open `model2.ipynb` and run all cells.
3. Make sure `panel` and `bokeh` are installed.
4. You’ll see an interactive dropdown to select each parking lot and view pricing over time.

---

## 📌 Conclusion

This project demonstrates a full **real-time dynamic pricing system** using streaming data, practical domain logic, and live visualization. Both models give meaningful and explainable results.

Model 2, in particular, shows the potential of **adaptive pricing** that responds to real-world congestion, demand, and special conditions—paving the way for smarter urban infrastructure.

---

## 🙌 Contributors

**Prem Anandh**  
Summer Analytics 2025 – Indian Institute of Technology Patna  
