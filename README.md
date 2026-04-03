# Supply Chain Analytics Notebook Guide

This repository contains a consolidated, end-to-end supply chain analytics notebook:

- `supply-chain-analysis.ipynb`

It analyzes delivery performance, profitability, demand volatility, and inventory strategy using the DataCo supply chain dataset.

## Dataset Used

- `dataset/DataCoSupplyChainDataset.csv`
- Optional metadata/reference files:
  - `dataset/DescriptionDataCoSupplyChain.csv`
  - `dataset/tokenized_access_logs.csv`

## Download Dataset (Kaggle)

Source:

- https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis?hl=en-IN

### What to download

From the Kaggle dataset download (ZIP), extract at least:

- `DataCoSupplyChainDataset.csv` (**required**)

Optional but useful:

- `DescriptionDataCoSupplyChain.csv`
- `tokenized_access_logs.csv` (if present in your downloaded package)

### Where to put files

Place files inside this project folder:

- `dataset/`

Expected structure:

```text
Supply Chain Analytics/
├── supply-chain-analysis.ipynb
├── requirements.txt
└── dataset/
    ├── DataCoSupplyChainDataset.csv
    ├── DescriptionDataCoSupplyChain.csv
    └── tokenized_access_logs.csv
```

### Important note

The notebook currently reads:

```python
path = "./dataset/DataCoSupplyChainDataset.csv"
```

So `DataCoSupplyChainDataset.csv` must exist in `dataset/` with the same filename.

### Quick setup options

#### Option A: Manual download (UI)

1. Open the Kaggle link.
2. Click **Download**.
3. Extract the ZIP.
4. Copy the CSV file(s) into `dataset/`.

#### Option B: Kaggle CLI

```bash
kaggle datasets download -d shashwatwork/dataco-smart-supply-chain-for-big-data-analysis -p dataset
unzip dataset/dataco-smart-supply-chain-for-big-data-analysis.zip -d dataset
```

If the ZIP filename differs, unzip the actual downloaded filename in `dataset/`.

## What the Notebook Contains

### 1) Setup & Data Loading

- Imports core libraries: `numpy`, `pandas`, `matplotlib`, `seaborn`.
- Loads dataset from `./dataset/DataCoSupplyChainDataset.csv`.
- Prints dataset shape and source date range.

### 2) Data Preparation & Standardization

- Parses order and shipping datetime columns with mixed-format-safe parsing.
- Builds standardized fields like:
  - `order_date`, `ship_date`, `lead_time_days`
  - `category`, `region`, `shipping_mode`, `customer_segment`, `sales`, `profit`, `quantity`, etc.
- Converts numeric columns, removes duplicates, and reports missing/unparsed values.

### 3) Section 1 — Supply Chain Reliability & Delivery Performance

- **Late Delivery by Shipping Mode**
  - Calculates total orders, late orders, late %, sales, profit, average lead time.
  - Visualization: bar charts for late rate and order/profit comparison.
- **Late Deliveries by Product Category**
  - Identifies highest-risk categories.
  - Visualization: category late % and sales-vs-profit views.
- **Bullwhip Effect (Demand Volatility)**
  - Computes coefficient of variation (CV) by category.
  - Flags risk bands (`CRITICAL`, `HIGH`, `NORMAL`).
  - Visualization: horizontal risk chart with threshold lines.
- **Regional Performance KPIs**
  - Tracks order volume, late %, sales, profit, lead time, and profit margin by region.
  - Visualization: 4-panel regional KPI dashboard.

### 4) Section 2 — Customer Profitability & Business Performance

- **Order Status Analysis**
  - Breakdown of statuses, including `PENDING_PAYMENT` impact.
  - Visualization: pie + financial bar comparison.
- **Customer Segment Profitability**
  - KPIs by customer segment (order count, revenue, profit, margin, late %).
  - Visualization: 2x2 segment performance dashboard.
- **Top Performing & At-Risk Product Categories**
  - Top and bottom categories by profit.
  - Visualization: profit ranking and profitability-vs-volume scatter.

### 5) Section 3 — Inventory & ABC-XYZ Segmentation

- **ABC-XYZ Segmentation**
  - ABC classes by cumulative sales contribution.
  - XYZ classes by demand variability.
  - Segment-level summary (orders, sales, profit, item count, sales share).
  - Visualization: class distribution + sales impact vs profitability bubble chart.
- **EOQ & Reorder Point Optimization**
  - Calculates EOQ, annual ordering/holding costs, reorder point, and safety stock assumptions.
  - Estimates total inventory cost and potential savings.
  - Visualization: ordering-vs-holding costs and EOQ recommendation scatter.

### 6) Section 4 — Strategy & Reporting Outputs

- **Executive Action Plan** with phased priorities:
  - Delivery reliability
  - Payment bottlenecks
  - Profitability recovery
  - Inventory and forecasting optimization
  - Customer segment strategy
- **KPI Dashboard Summary**
  - Financial, operations, payment/cash flow, profitability, demand/inventory metrics.
- **Conclusion Block**
  - Consolidated summary and practical next steps.

## Visual Outputs in Notebook

The notebook generates multiple management-ready visuals, including:

- Late delivery risk dashboards
- Category performance diagnostics
- Bullwhip risk charts
- Regional KPI panels
- Order status and segment profitability charts
- ABC-XYZ and EOQ optimization visuals

## How to Run

1. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

2. Launch Jupyter:

   ```bash
   jupyter notebook
   ```

3. Open `supply-chain-analysis.ipynb` and run cells top-to-bottom.

## Requirements

Main packages (see full list in `requirements.txt`):

- `numpy`, `pandas`
- `matplotlib`, `seaborn`, `plotly`
- `scikit-learn`, `scipy`, `statsmodels`
- `xgboost`, `prophet`

## Notes

- The notebook is designed as a consolidated business report plus technical analysis.
- It is suitable for executive review, operational diagnostics, and data science handoff.
