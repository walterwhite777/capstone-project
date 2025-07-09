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

---<img width="754" alt="Screenshot 2025-07-09 at 11 27 51 PM" src="https://github.com/user-attachments/assets/9f374623-a983-4e32-a922-95902d7406de" />
<img width="750" alt="Screenshot 2025-07-09 at 11 28 01 PM" src="https://github.com/user-attachments/assets/23858067-7d4a-4353-beb9-0cffb97a3ca2" />
<img width="754" alt="Screenshot 2025-07-09 at 11 28 08 PM" src="https://github.com/user-attachments/assets/f079e9b5-4066-4e2b-962a-1c37ccd5f7be" />
<img width="754" alt="Screenshot 2025-07-09 at 11 28 15 PM" src="https://github.com/user-attachments/assets/a762606e-e29a-4af0-9c5d-d617e8101213" />
<img width="750" alt="Screenshot 2025-07-09 at 11 28 21 PM" src="https://github.com/user-attachments/assets/888f014d-82a1-460a-ac68-e235f08590bf" />
<img width="753" alt="Screenshot 2025-07-09 at 11 28 28 PM" src="https://github.com/user-attachments/assets/851ff450-0013-410c-9e74-0e686ef32d08" /><img width="755" alt="Screenshot 2025-07-09 at 11 26 54 PM" src="https://github.com/user-attachments/assets/1821d7fc-9763-475e-b4c9-cdac7e1d7c4c" />
<img width="752" alt="Screenshot 2025-07-09 at 11 27 06 PM" src="https://github.com/user-attachments/assets/043eb151-adb5-4f82-a577-4277175b68c3" />
<img width="752" alt="Screenshot 2025-07-09 at 11 27 14 PM" src="https://github.com/user-attachments/assets/93f41e07-b9fd-43e8-8032-02269eb3068f" />
<img width="753" alt="Screenshot 2025-07-09 at 11 27 26 PM" src="https://github.com/user-attachments/assets/cd2b2aae-8323-49c4-b975-b0d2b8c71129" />
<img width="751" alt="Screenshot 2025-07-09 at 11 27 35 PM" src="https://github.com/user-attachments/assets/18f46ac0-5602-42a3-9692-8148be3bd26d" />
<img width="754" alt="Screenshot 2025-07-09 at 11 27 44 PM" src="https://github.com/user-attachments/assets/737d3c80-44dc-4cad-b2e9-8fe0c9fff83d" />
<img width="748" alt="Screenshot 2025-07-09 at 11 26 38 PM" src="https://github.com/user-attachments/assets/d11bf493-a213-4dc4-a395-f931ed754a5e" />
<img width="749" alt="Screenshot 2025-07-09 at 11 26 46 PM" src="https://github.com/user-attachments/assets/d331d297-195e-47bf-9d1e-6c1ea25ed0dc" />



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
<img width="1017" alt="Screenshot 2025-07-10 at 12 11 12 AM" src="https://github.com/user-attachments/assets/9801cf83-1482-4cbf-abfa-0f88681aa2b4" />

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
