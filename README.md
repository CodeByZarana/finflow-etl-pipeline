# Financial Data ETL Pipeline

A production-ready ETL pipeline for processing financial transaction data, implementing data quality checks, dimensional modeling, and automated feed generation.

## 🎯 Project Overview

This project demonstrates end-to-end data engineering practices for financial services:
- **Extract**: Data ingestion from APIs and file sources
- **Transform**: Data cleaning, validation, and business rule application
- **Load**: Star schema implementation for analytics

Built with Python, SQL, FastAPI, and designed for AWS deployment.

## 🏗️ Architecture
```
Data Sources → Extraction → Validation → Transformation → Star Schema → API/Feeds
     ↓            ↓            ↓             ↓              ↓            ↓
  CSV/API     Pandas      Data Quality   Business      Fact/Dim     FastAPI
              Python      Checks         Rules         Tables       Endpoints
```

## 🚀 Features

- **Data Profiling**: Automated data quality assessment
- **Data Cleaning**: Handle missing values, standardize formats
- **Business Rules**: Financial calculations and categorizations
- **Dimensional Modeling**: Star schema with fact and dimension tables
- **API Layer**: FastAPI endpoints for pipeline control and data access
- **Error Handling**: Comprehensive logging and retry mechanisms
- **Testing**: Unit tests for all transformation logic
- **Documentation**: Complete data dictionary and architecture docs

## 💻 Tech Stack

- **Python 3.11+**: Core language
- **Pandas**: Data manipulation
- **SQLite/PostgreSQL**: Database storage
- **FastAPI**: API framework
- **Pytest**: Testing framework
- **AWS Services**: S3, Lambda, Glue (deployment ready)

## 📦 Installation
```bash
# Clone repository
git clone https://github.com/yourusername/financial-data-etl-pipeline.git
cd financial-data-etl-pipeline

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Generate sample data
python scripts/generate_sample_data.py

# Run ETL pipeline
python scripts/run_etl.py
```

## 🎮 Usage

### Run Complete Pipeline
```bash
python scripts/run_etl.py --input data/raw/transactions.csv
```

### Start API Server
```bash
cd api
uvicorn main:app --reload
# Visit http://localhost:8000/docs for interactive API documentation
```

### Run Tests
```bash
pytest tests/
```

## 📊 Pipeline Steps

### 1. Data Profiling
```python
from src.transformation.data_profiling import profile_data
profile_results = profile_data('data/raw/transactions.csv')
```

### 2. Data Cleaning
```python
from src.transformation.data_cleaning import clean_transaction_data
clean_df = clean_transaction_data(raw_df)
```

### 3. Business Transformations
```python
from src.transformation.business_rules import apply_business_rules
transformed_df = apply_business_rules(clean_df)
```

### 4. Star Schema Creation
```python
from src.loading.star_schema import create_star_schema
dimensions, fact_table = create_star_schema(transformed_df)
```

## 🌟 Star Schema Design

**Fact Table**: `transactions_fact`
- Transaction-level metrics
- Foreign keys to dimension tables

**Dimension Tables**:
- `customer_dimension`: Customer information and risk profiles
- `account_dimension`: Account details and types
- `security_dimension`: Security master data
- `date_dimension`: Date attributes for time-based analysis

## 📈 Sample Queries
```sql
-- Monthly trading volume by asset class
SELECT 
    d.year,
    d.month,
    s.asset_class,
    SUM(f.net_amount) as total_volume
FROM transactions_fact f
JOIN date_dimension d ON f.trade_date_sk = d.date_sk
JOIN security_dimension s ON f.security_sk = s.security_sk
GROUP BY d.year, d.month, s.asset_class;
```

## 🚀 AWS Deployment

The pipeline is designed for AWS deployment:
- **S3**: Store raw and processed data
- **Lambda**: Serverless ETL execution
- **Glue**: Data cataloging and orchestration
- **Redshift**: Data warehouse for star schema

See [docs/deployment_guide.md](docs/deployment_guide.md) for details.

## 🧪 Testing
```bash
# Run all tests
pytest tests/ -v

# Run with coverage
pytest tests/ --cov=src --cov-report=html
```

## 📚 Documentation

- [Architecture Overview](docs/architecture.md)
- [Data Dictionary](docs/data_dictionary.md)
- [Deployment Guide](docs/deployment_guide.md)

## 🎓 Learning Outcomes

This project demonstrates:
- ✅ ETL pipeline design and implementation
- ✅ Data quality validation and error handling
- ✅ Dimensional modeling (star schema)
- ✅ RESTful API development with FastAPI
- ✅ Cloud-ready architecture (AWS)
- ✅ Production best practices (logging, testing, documentation)

## 📧 Contact

Zarana Solanki - zaranasolanki41014@gmail.com

LinkedIn: [linkedin.com/in/zarana-solanki](https://linkedin.com/in/zarana-solanki)

Portfolio: [Your Portfolio Link]
