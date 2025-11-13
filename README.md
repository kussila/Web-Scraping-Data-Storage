# 📚 Web Scraping ETL Pipeline: Book Data Ingestion

## 🎯 Project Overview

This repository contains a complete **Extract, Transform, Load (ETL)** pipeline written in Python. The goal of the project is to reliably ingest current product data (titles, prices, and ratings) from a static e-commerce sample site, perform essential data cleaning, and persist the results to a clean CSV file for downstream reporting and analysis.

### 🛠️ Tech Stack

| Tool | Purpose |
| :--- | :--- |
| **Python** | Core language for the pipeline logic |
| **requests** | Handles HTTP GET requests to fetch raw HTML |
| **BeautifulSoup4**| Parses and navigates HTML structure |
| **Pandas** | Structures and cleans extracted data into a DataFrame |

---

## ⚙️ Setup and Execution

### 1. Environment Setup

It is highly recommended to run this project within a **virtual environment (`venv`)** to manage dependencies.

```bash
# Create the virtual environment
python -m venv data_env 

# Activate the environment (Windows)
data_env\Scripts\activate 
````

### 2\. Required Libraries

If you do not use a `requirements.txt`, run the following command to install the required libraries:

```bash
(data_env) pip install requests beautifulsoup4 pandas
```

### 3\. Running the Pipeline

Execute the main script (or your notebook file) to start the ETL process:

```bash
(data_env) python scraper.py
```

-----

## 📈 ETL Pipeline Breakdown

The pipeline is structured to ensure clean separation of concerns and robust data handling.

### E - Extraction

  * The `requests` library sends a **GET** request to the target URL (`http://books.toscrape.com/`).
  * A status code check (`response.status_code == 200`) ensures successful extraction before proceeding.

### T - Transformation & Parsing

  * **HTML Parsing:** `BeautifulSoup` converts the raw HTML string into a nested, navigable Python object.
  * **Selector Logic:** The script uses **CSS selectors** (`<article class="product_pod">`) to accurately locate and iterate through each book item.
  * **Data Extraction:** The `.find()` method is used within each container to extract specific data points:
      * `Title`: Extracted from the `h3/a` tag.
      * `Price`: Extracted from the `<p class="price_color">` tag.
      * `Rating`: Extracted via the `star-rating` class.
  * **Structuring:** Extracted data is organized into a **Pandas DataFrame** for final persistence.

### L - Load

  * The final, structured DataFrame is saved to a clean **CSV file** named `book_report.csv`.
  * The `index=False` parameter is used to prevent writing unnecessary index columns to the output file.

-----

## 📊 Data Output

The pipeline generates the `book_report.csv` file, with the following structure:

| Title | Price | Rating |
| :--- | :--- | :--- |
| A Light in the Attic | £51.77 | Three |
| Tipping the Velvet | £53.74 | One |
| ... | ... | ... |
| The Secret Garden | £15.00 | Four |