# PANDUAN SETUP PROJECT: University Analytics Dashboard

## 📋 Daftar Isi
1. [Overview](#overview)
2. [Prasyarat](#prasyarat)
3. [Instalasi](#instalasi)
4. [Struktur Project](#struktur-project)
5. [Menggunakan Setup Script](#menggunakan-setup-script)
6. [Troubleshooting](#troubleshooting)

---

## Overview

Setup script (`setup.sh`) adalah automated installer untuk inisialisasi project University Analytics Dashboard dengan struktur lengkap dan dependencies yang sudah terinstall.

**Fitur yang disediakan:**
- ✅ Automated directory structure creation
- ✅ Python virtual environment setup
- ✅ Dependency installation via pip
- ✅ Configuration files generation
- ✅ Template files untuk app, database, dan utilities
- ✅ Sample Jupyter notebook
- ✅ Unit test templates
- ✅ Git-ready project structure

---

## Prasyarat

### Minimum Requirements
- **OS**: macOS, Linux, atau Windows (dengan Git Bash/WSL)
- **Python**: 3.9 atau lebih tinggi
- **pip**: 21.0 atau lebih tinggi
- **git**: (optional, tapi recommended)
- **RAM**: Minimal 4GB
- **Disk Space**: Minimal 2GB free space

### Verifikasi Installation

```bash
# Check Python version
python3 --version

# Check pip
pip3 --version

# Check git (optional)
git --version
```

---

## Instalasi

### Method 1: Menggunakan Setup Script (Recommended)

#### Step 1: Clone atau Download Project

```bash
# Clone dari GitHub (jika tersedia)
git clone <repository-url>
cd university_dashboard

# Atau, jika menggunakan file manual:
# 1. Download semua files ke folder
# 2. Buka terminal
# 3. cd ke folder project
```

#### Step 2: Make Setup Script Executable (Linux/macOS)

```bash
chmod +x setup.sh
```

#### Step 3: Run Setup Script

```bash
./setup.sh
```

**Windows (Git Bash):**
```bash
bash setup.sh
```

#### Step 4: Ikuti Output Script

Script akan menampilkan progress dengan warna:
- 🟢 GREEN = Success
- 🔴 RED = Error
- 🟡 YELLOW = Info/Warning
- 🔵 BLUE = Section Header

---

### Method 2: Manual Setup

Jika setup script tidak berfungsi:

```bash
# Create virtual environment
python3 -m venv .venv

# Activate virtual environment
# Linux/macOS:
source .venv/bin/activate

# Windows:
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Create directories manually
mkdir -p src/dashboard src/data src/utils
mkdir -p notebooks docs database config
mkdir -p images/screenshots images/mockups
mkdir -p output/reports output/exports
mkdir -p tests .github/workflows

# Copy configuration files from the setup script output
```

---

## Struktur Project

Setelah setup, project akan memiliki struktur berikut:

```
university_dashboard/
│
├── .venv/                              # Virtual environment
│   ├── bin/                           # Executables (Linux/macOS)
│   └── Scripts/                       # Executables (Windows)
│
├── src/                                # Source code
│   ├── __init__.py
│   ├── dashboard/
│   │   ├── __init__.py
│   │   └── app.py                    # Main Streamlit application
│   ├── data/
│   │   ├── __init__.py
│   │   └── loader.py                 # Data loading utilities
│   └── utils/
│       ├── __init__.py
│       └── helpers.py                # Helper functions
│
├── notebooks/
│   ├── 00_setup.ipynb
│   ├── 01_data_exploration.ipynb     # Data exploration
│   ├── 02_data_cleaning.ipynb        # Data cleaning & preprocessing
│   ├── 03_visualization.ipynb        # Visualization experiments
│   └── 04_analysis.ipynb             # Statistical analysis
│
├── docs/
│   ├── README.md                     # Main documentation
│   ├── SETUP.md                      # Setup documentation
│   ├── API.md                        # API reference
│   ├── ARCHITECTURE.md               # Architecture design
│   └── CONTRIBUTING.md               # Contributing guidelines
│
├── database/
│   ├── university.db                 # SQLite database (created later)
│   ├── data/
│   │   ├── students.csv              # Sample data (generated)
│   │   ├── programs.csv              # Program data
│   │   ├── courses.csv               # Course data
│   │   └── enrollments.csv           # Enrollment data
│   └── schemas/
│       └── schema.sql                # Database schema
│
├── images/
│   ├── screenshots/                  # Dashboard screenshots
│   └── mockups/                      # UI mockups
│
├── output/
│   ├── reports/                      # Generated reports
│   └── exports/                      # Data exports
│
├── tests/
│   ├── __init__.py
│   ├── test_data_loader.py           # Unit tests
│   └── test_app.py                   # App tests
│
├── config/
│   ├── config.py                     # Configuration module
│   └── settings.json                 # Settings file
│
├── scripts/
│   ├── generate_sample_data.py       # Generate sample data
│   ├── init_database.py              # Initialize database
│   └── data_import.py                # Import data
│
├── .github/
│   └── workflows/                    # CI/CD workflows (optional)
│
├── .env                              # Environment variables
├── .gitignore                        # Git ignore patterns
├── requirements.txt                  # Python dependencies
├── setup.sh                          # Setup script
├── run.sh                            # Run dashboard script
├── README.md                         # Project README
├── SETUP_SUMMARY.txt                 # Setup summary
└── pytest.ini                        # Pytest configuration
```

---

## Menggunakan Setup Script

### Tahap-Tahap Setup Script

#### **Tahap 1: Cek Prerequisites**
```
Checking Python 3 installation
Checking pip installation  
Checking git installation (optional)
```

#### **Tahap 2: Membuat Struktur Direktori**
```
Creating directories:
- .venv/
- src/dashboard/, src/data/, src/utils/
- notebooks/
- docs/
- database/data/, database/schemas/
- images/
- output/
- tests/
- config/
```

#### **Tahap 3: Setup Python Virtual Environment**
```
Creating virtual environment (.venv)
Activating virtual environment
Upgrading pip, setuptools, wheel
```

#### **Tahap 4: Install Dependencies**
```
Creating requirements.txt
Installing packages:
- streamlit, dash, plotly (Web frameworks)
- pandas, numpy, scipy (Data processing)
- sqlalchemy, sqlite (Database)
- matplotlib, seaborn, altair (Visualization)
- scikit-learn, statsmodels (ML & Analytics)
- pytest, black, flake8 (Testing & Code quality)
- jupyter, ipython (Notebooks)
```

#### **Tahap 5: Buat Konfigurasi & Template**
```
Creating .env file
Creating config/config.py
Creating src/dashboard/app.py
Creating src/data/loader.py
Creating __init__.py files
```

#### **Tahap 6: Buat Database Schema**
```
Creating database/schemas/schema.sql
- Students table
- Programs table
- Faculty table
- Courses table
- Enrollments table
```

#### **Tahap 7: Dokumentasi**
```
Creating README.md
Creating CONTRIBUTING.md
Creating .gitignore
```

#### **Tahap 8: Sample Notebook**
```
Creating notebooks/01_data_exploration.ipynb
```

#### **Tahap 9: Test Files**
```
Creating tests/test_data_loader.py
```

#### **Tahap 10: Helper Scripts**
```
Creating run.sh
Creating scripts/generate_sample_data.py
```

---

## Post-Installation Setup

### 1. Activate Virtual Environment

**Linux/macOS:**
```bash
source .venv/bin/activate
```

**Windows (Command Prompt):**
```bash
.venv\Scripts\activate.bat
```

**Windows (PowerShell):**
```bash
.venv\Scripts\Activate.ps1
```

**Verifikasi aktivasi:**
```bash
# Prompt akan menunjukkan (.venv) di depan
# Contoh: (.venv) user@computer:~/university_dashboard$
```

### 2. Generate Sample Data (Optional)

```bash
# Pastikan virtual environment aktif
python scripts/generate_sample_data.py
```

Ini akan membuat:
- `database/data/students.csv` - 100 sample students
- `database/data/programs.csv` - 10 sample programs

### 3. Verifikasi Installation

```bash
# List installed packages
pip list

# Run pytest to verify
pytest tests/

# Check Python path
which python  # Linux/macOS
where python  # Windows
```

---

## Menjalankan Dashboard

### Option 1: Menggunakan Run Script

```bash
./run.sh
```

### Option 2: Direct Streamlit Command

```bash
streamlit run src/dashboard/app.py
```

**Output yang diharapkan:**
```
  You can now view your Streamlit app in your browser.

  Local URL: http://localhost:8501
  Network URL: http://192.168.x.x:8501
```

Buka browser dan pergi ke: **http://localhost:8501**

---

## Perintah-Perintah Berguna

### Development

```bash
# Activate virtual environment
source .venv/bin/activate

# Install new package
pip install package_name

# Update dependencies
pip install --upgrade -r requirements.txt

# View installed packages
pip list

# Freeze dependencies
pip freeze > requirements.txt
```

### Testing

```bash
# Run all tests
pytest

# Run with verbosity
pytest -v

# Run specific test file
pytest tests/test_data_loader.py

# Generate coverage report
pytest --cov=src tests/
```

### Code Quality

```bash
# Format code
black src/

# Check code style
flake8 src/

# Lint code
pylint src/

# Check complexity
radon cc src/
```

### Jupyter Notebook

```bash
# Start Jupyter
jupyter notebook

# Start JupyterLab
jupyter lab
```

### Database

```bash
# Initialize database
python scripts/init_database.py

# Import data
python scripts/data_import.py
```

### Deactivate Virtual Environment

```bash
deactivate
```

---

## Troubleshooting

### Problem: Python 3 not found

**Solution:**
```bash
# Check installation
python3 --version

# If not installed, install from python.org
# Or use package manager:
# macOS: brew install python3
# Ubuntu: sudo apt-get install python3
# Windows: Download from python.org
```

### Problem: Permission Denied (setup.sh)

**Solution (Linux/macOS):**
```bash
chmod +x setup.sh
./setup.sh
```

### Problem: Virtual Environment not activating

**Solution:**
```bash
# Reinstall venv
rm -rf .venv
python3 -m venv .venv
source .venv/bin/activate
```

### Problem: Pip install fails

**Solution:**
```bash
# Upgrade pip
pip install --upgrade pip

# Install with verbose output
pip install -v -r requirements.txt

# Try installing individually
pip install streamlit
pip install pandas
# ... dll
```

### Problem: Database Error

**Solution:**
```bash
# Delete corrupted database
rm database/university.db

# Reinitialize
python scripts/init_database.py
```

### Problem: Port 8501 already in use

**Solution:**
```bash
# Use different port
streamlit run src/dashboard/app.py --server.port 8502
```

### Problem: ModuleNotFoundError

**Solution:**
```bash
# Ensure virtual environment is activated
source .venv/bin/activate  # or appropriate command

# Reinstall requirements
pip install -r requirements.txt
```

---

## Deactivasi Setup

Jika ingin membersihkan project:

```bash
# Deactivate virtual environment
deactivate

# Remove virtual environment
rm -rf .venv

# Remove database
rm database/university.db

# Remove generated data
rm database/data/*.csv
```

---

## Next Steps

Setelah setup berhasil, Anda siap untuk:

1. **Explore data**: Buka `notebooks/01_data_exploration.ipynb`
2. **Design dashboard**: Modify `src/dashboard/app.py`
3. **Add features**: Tambah pages dan visualizations
4. **Test code**: Tulis unit tests di `tests/`
5. **Push to Git**: Commit dan push ke repository

---

## Resources

- **Streamlit Docs**: https://docs.streamlit.io
- **Pandas Docs**: https://pandas.pydata.org/docs
- **Plotly Docs**: https://plotly.com/python
- **Python Virtual Env**: https://docs.python.org/3/tutorial/venv.html

---

**Last Updated**: December 2025  
**Setup Version**: 1.0.0
