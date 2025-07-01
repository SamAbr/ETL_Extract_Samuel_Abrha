# Full vs. Incremental Extractions — ETL Project

**Name:** Samuel Abrha Gebremariam  
**ID:** ***533

---

## Project Description

This project demonstrates the difference between **Full Extraction** and **Incremental Extraction** within an ETL (Extract, Transform, Load) pipeline using Python and Jupyter Notebook.

The workflow involves:
- Extracting Google's 5-year historical stock price data
- Cleaning and transforming the data
- Simulating an incremental update scenario
- Saving both transformed datasets
- Loading the datasets into structured formats using SQLite and Parquet

---

## Files Included

| File | Description |
|------|-------------|
| `etl_extract.ipynb` | Main Jupyter Notebook containing extraction, transformation, and saving logic |
| `etl_load.ipynb` | Loads transformed data into SQLite and Parquet formats |
| `google_5yr_one.csv` | Original 5-year stock data for Google |
| `last_extraction.txt` | Stores the timestamp of the last successful extraction |
| `Download/transformed_full.csv` | Cleaned and transformed full dataset |
| `Download/transformed_incremental.csv` | Transformed data representing new/updated entries |
| `loaded_data/full_data.db` | SQLite database for full data |
| `loaded_data/incremental_data.db` | SQLite database for incremental data |
| `loaded_data/full_data.parquet` | Parquet file for full data |
| `loaded_data/incremental_data.parquet` | Parquet file for incremental data |
| `.gitignore` | Prevents tracking of unnecessary or large files like `.db`, `.parquet`, and `loaded_data/` |
| `README.md` | This project overview and instructions |

---

## Tools Used

- Python
- Pandas
- SQLite3
- Parquet (via pandas)
- Jupyter Notebook
- GitHub Desktop (for version control)

---

## ETL Process Overview

### 1. **Full Extraction & Transformation**

- **Step 1**: Load full dataset from `google_5yr_one.csv`
- **Step 2**: Drop malformed row (incorrectly parsed header)
- **Step 3**: Convert column data types (e.g., `Close`, `High`, `Low`, `Volume`)
- **Step 4**: Remove duplicates and check for missing values
- **Step 5**: Add a new column `price_range` based on `Close` price:
  - Bins: `[0–100, 100–150, 150–200, 200+]`
  - Labels: `Low`, `Medium`, `High`, `Very High`
- **Step 6**: Save to `Download/transformed_full.csv`

### 2. **Incremental Extraction & Transformation**

- Simulated by extracting data from a certain date
- Same transformation steps as full extraction:
  - Checking for missing values and duplicates
  - Data type correction
  - `price_range` creation
- Save as `Download/transformed_incremental.csv`

---

## Transformations included in the task

- Cleaning: Handling missing values and duplicates (The dataset did not have any missing values or duplicates though)
- Structural: Convert data types, standardize date formats.
- Categorization: Bin numerical values (binned the Close column)

---

## Dataset

- **Source**: Kaggle
- **Data**: Google stock prices over 5 years
- **Fields**:
  - `Date`, `Open`, `High`, `Low`, `Close`, `Volume`

---

## How to Run

1. **Clone this repository** using GitHub Desktop or `git clone`.
2. Ensure the following files are in the same directory:
   - `etl_extract.ipynb`
   - `etl_load.ipynb`
   - `google_5yr_one.csv`
   - `last_extraction.txt`
3. Launch **Jupyter Notebook** through Anaconda or VS Code.
4. Open `etl_extract.ipynb` and run all cells to:
   - Perform full extraction and transformation
   - Simulate incremental extraction and update
5. Open `etl_load.ipynb` and run all cells to:
   - Load both datasets into SQLite databases
   - Save the datasets as Parquet files

---

## Outputs

- **Cleaned Full Dataset**: `Download/transformed_full.csv`
- **Cleaned Incremental Dataset**: `Download/transformed_incremental.csv`
- **SQLite Databases**:
  - `loaded_data/full_data.db`
  - `loaded_data/incremental_data.db`
- **Parquet Files**:
  - `loaded_data/full_data.parquet`
  - `loaded_data/incremental_data.parquet`

---

## Loading Details

Both `transformed_full.csv` and `transformed_incremental.csv` were loaded into:

| Dataset | SQLite Table | SQLite DB Path | Parquet Path |
|---------|--------------|----------------|--------------|
| Full | `full_data` | `loaded_data/full_data.db` | `loaded_data/full_data.parquet` |
| Incremental | `incremental_data` | `loaded_data/incremental_data.db` | `loaded_data/incremental_data.parquet` |

### Sample Code

```python
df_full = pd.read_csv("Download/transformed_full.csv")
df_full.to_sql("full_data", sqlite3.connect("loaded_data/full_data.db"), if_exists="replace", index=False)
df_full.to_parquet("loaded_data/full_data.parquet", index=False)
```

## Learning Objectives Demonstrated

- Data cleaning and type correction
- Full vs. incremental data pipeline logic
- Use of conditions (`pd.cut`) for feature creation
- Exporting structured data
- Loading data into SQLite and Parquet formats
- File structure organization and automation

---

## Screenshots

  ![image](https://github.com/user-attachments/assets/a3f5a003-c9aa-471d-b87a-2cc1cd6750cb)
  ![image](https://github.com/user-attachments/assets/18ca725f-3ea1-44e5-b652-9c6fc27c0287)
  ![image](https://github.com/user-attachments/assets/ae0f8663-db02-418f-8336-ec241124d855)
  ![image](https://github.com/user-attachments/assets/f7ed4c6f-05b1-44b9-9861-3c389eb195e1)


