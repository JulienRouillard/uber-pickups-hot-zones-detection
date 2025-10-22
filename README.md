# Uber Pickups - Hot Zones Detection

**Machine Learning project for identifying optimal driver positioning zones in New York City using unsupervised clustering algorithms.**

## 📊 Project Overview

This project analyzes Uber pickup data to identify **hot zones** where driver demand is highest at specific times. By clustering pickup locations, the solution helps optimize driver distribution across NYC.

### Key Results

- **168 hot-zone maps** generated (7 days × 24 hours)
- **DBScan clustering** selected for superior outlier handling and adaptive cluster detection
- **Automatic parameter tuning** using k-distance method for epsilon estimation

<p align="center">
  <img src="maps/mercredi_14_15.png" alt="Thursday between 2 PM and 3 PM" width="45%">
  <img src="maps/vendredi_22_23.png" alt="Friday between 10 PM and 11 PM" width="45%">
  <br>
  <em>Example: Hot zones comparison between Thursday and Friday at different hours</em>
</p>

## 🎯 Business Problem

Uber identified that drivers are often not positioned where demand is highest, leading to:
- **10-15 minute wait times** in certain neighborhoods
- **User cancellations** when wait exceeds 5-7 minutes
- **Inefficient driver distribution** across the city

**Solution**: Create an algorithm to recommend hot-zones where drivers should position themselves based on day of week and hour.

## 🔬 Methodology

### Algorithm Comparison

Two unsupervised learning algorithms were evaluated:

| Algorithm | Pros | Cons | Selected |
|-----------|------|------|----------|
| **KMeans** | Fast, well-defined clusters | Requires pre-defining k, sensitive to outliers | ❌ |
| **DBScan** | Auto-detects cluster count, handles outliers | Requires parameter tuning | ✅ |

**DBScan was selected** because:
- Automatically identifies optimal number of clusters
- Eliminates noise/outliers for clearer hot-zones
- Produces geographically coherent clusters

## 📁 Project Structure

```
uber-pickups-hot-zones-detection/
├── uber_pickups.ipynb      # Analysis notebook
├── requirements.txt        # Python dependencies
├── data/                   # Raw Uber pickup data (Apr-Sep 2014)
│   ├── uber-raw-data-apr14.csv
│   ├── uber-raw-data-may14.csv
│   └── ...
├── hot_zones/              # Generated clustering results
│   ├── lundi/              # Monday clusters (0_1.csv to 23_24.csv)
│   ├── mardi/              # Tuesday clusters
│   └── ...
└── maps/                   # Sample visualization maps (one per day)
    ├── lundi_7_8.png
    ├── mardi_5_6.png
    └── ...
```

## 🛠️ Installation

### Prerequisites

- Python 3.8 or higher
- Jupyter Notebook

### Setup

1. Clone the repository:
```bash
git clone https://github.com/JulienRouillard/uber-pickups-hot-zones-detection.git
cd uber-pickups-hot-zones-detection
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Launch Jupyter Notebook:
```bash
jupyter notebook uber_pickups.ipynb
```

## 🚀 Usage

### Quick Start - View Results

To visualize existing hot-zones:

```python
# Display hot-zones for Monday from 8 AM to 9 AM
get_map('lundi', 8)

# Display hot-zones for Friday FROM 6 PM to 7 PM
get_map('vendredi', 18)
```

### Full Pipeline - Regenerate Clusters

To recompute all hot-zones from scratch (⚠️ ~120 minutes):

```python
# Run the clustering loop in the notebook
for time in data_splited.keys():
    get_hot_zones(day=time[0], hour=time[1])
```

This will regenerate all 168 CSV files in `hot_zones/`.

## 💻 Technologies

- **Data Processing**: `pandas`, `numpy`
- **Machine Learning**: `scikit-learn` (KMeans, DBScan, StandardScaler)
- **Geospatial Analysis**: `geopandas`, `shapely`
- **Visualization**: `plotly`, `matplotlib`, `contextily`

## 📧 Contact

**Julien Rouillard**  
📫 julien.rouillard@yahoo.fr