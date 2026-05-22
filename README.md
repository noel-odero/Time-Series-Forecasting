# Comparative Time Series Analysis and Forecasting of Mobile Network Traffic

A complete machine learning pipeline for analyzing and forecasting mobile internet traffic
across the city of Milan, Italy, using the Telecom Italia Mobile (TIM) dataset.

## Project Overview

This project covers three main tasks:

- **Task 1**: Efficient handling and memory optimization of a 5GB dataset on a
  resource-constrained local machine
- **Task 2**: Exploratory data analysis including spatial, temporal, and statistical
  characterization of mobile traffic patterns
- **Task 3**: Design and comparison of three forecasting models (SARIMA, LSTM, Transformer)
  for one-step-ahead traffic prediction


## Dataset

The dataset is the Telecom Italia Mobile (TIM) Milan telecommunications activity dataset,
available from the Harvard Dataverse:

- Telecommunications activity data: https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/EGZHFV
- Grid data: https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/QJWLFU

The dataset consists of 62 plain-text files (~5GB total), one per day, covering November 1
to December 31, 2013. Only the `square_id`, `timestamp`, and `internet` columns are used.

**The raw data files are not included in this repository due to size.** Follow the setup
instructions below to download and prepare them.

## Requirements

- Python 3.10+
- ~4GB free disk space for the HDF5 file
- ~2GB RAM minimum available during processing

Install all dependencies:

```bash
pip install -r requirements.txt
```

## Setup Instructions

### Step 1: Clone the repository

```bash
git clone repo link
cd repo
```

### Step 2: Create and activate a virtual environment

```bash
python3 -m venv venv

# Linux / Mac
source venv/bin/activate

# Windows
venv\Scripts\activate
```

### Step 3: Install dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Download the dataset

Go to the Harvard Dataverse link above and download all 62 files from the
Telecommunications activity dataset. Place all zip files into a folder on your machine,
for example:

```
/home/yourname/dataverse/
```

### Step 5: Update the paths in the notebook

Open `milan_traffic_analysis.ipynb` and update Cell 4 with your actual paths:

```python
ZIP_DIR      = '/home/yourname/dataverse/'
RAW_DIR      = '/home/yourname/dataverse/raw_data'
HDF_PATH     = '/home/yourname/dataverse/milan_traffic.h5'
FIGURES_DIR  = '/home/yourname/dataverse/figures'
```

### Step 6: Run the notebook

Open the notebook in VS Code or Jupyter and run all cells:

```bash
jupyter notebook milan_traffic_analysis.ipynb
```

Or open in VS Code and click **Run All**.

**First run:** The notebook will extract the zip files, process all 62 daily files
incrementally, and write the HDF5 file to disk. This takes approximately 15-30 minutes
depending on your machine.

**Subsequent runs:** The notebook detects the existing HDF5 file and skips directly to
loading, taking only a few seconds.

## Reproducing the Results

The test period is strictly **December 16-22, 2013**. The three geographical areas
analyzed are:

| Area | Square ID | Description |
|------|-----------|-------------|
| Highest traffic | 5161 | Highest total CDR count over two months |
| Fixed area 1 | 4159 | Specified in assignment |
| Fixed area 2 | 4556 | Specified in assignment |


## Key Results

| Model | MAE (Square 5161) | RMSE (Square 5161) |
|-------|-------------------|---------------------|
| SARIMA | 2400.757 | 3456.141 |
| LSTM | 84.579 | 136.826 |
| Transformer | 118.850 | 156.850 |

The LSTM achieved the best overall performance across all three areas.



## References

[1] G. Barlacchi et al., "A multi-source dataset of urban life in the city of Milan and
the Province of Trentino," Sci. Data, vol. 2, p. 150055, 2015.

[2] S. Hochreiter and J. Schmidhuber, "Long Short-Term Memory," Neural Comput., vol. 9,
no. 8, pp. 1735-1780, 1997.

[3] A. Vaswani et al., "Attention Is All You Need," in Advances in Neural Information
Processing Systems, vol. 30, 2017.




