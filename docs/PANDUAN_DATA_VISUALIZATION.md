# 📊 PANDUAN LENGKAP: PROJECT DATA FOLDER & DATA VISUALIZATION

## 📋 Daftar Isi
1. [Struktur Project Data Folder](#struktur-project-data-folder)
2. [Setup Data Folder](#setup-data-folder)
3. [Data Sources & Collection](#data-sources--collection)
4. [Data Cleaning & Preparation](#data-cleaning--preparation)
5. [Data Visualization Design](#data-visualization-design)
6. [Implementation Langkah-Langkah](#implementation-langkah-langkah)
7. [Best Practices](#best-practices)

---

## 📁 Struktur Project Data Folder

### Rekomendasi Struktur Lengkap:

```
university_dashboard/
├── database/
│   ├── data/                           # ← DATA FOLDER UTAMA
│   │   ├── raw/                        # Raw data (as received)
│   │   │   ├── students_raw.csv
│   │   │   ├── programs_raw.xlsx
│   │   │   ├── enrollments_raw.csv
│   │   │   └── faculty_raw.csv
│   │   │
│   │   ├── processed/                  # Cleaned & processed data
│   │   │   ├── students_cleaned.csv
│   │   │   ├── programs_cleaned.csv
│   │   │   ├── enrollments_cleaned.csv
│   │   │   └── faculty_cleaned.csv
│   │   │
│   │   ├── aggregated/                 # Aggregated for visualization
│   │   │   ├── enrollment_by_program.csv
│   │   │   ├── student_demographics.csv
│   │   │   ├── program_statistics.csv
│   │   │   └── financial_summary.csv
│   │   │
│   │   └── metadata/                   # Data documentation
│   │       ├── data_dictionary.md
│   │       ├── data_quality_report.md
│   │       └── update_log.txt
│   │
│   ├── schemas/
│   │   └── schema.sql
│   │
│   └── university.db                   # SQLite database
│
├── src/
│   ├── data/
│   │   ├── __init__.py
│   │   ├── loader.py                   # Load data dari files/database
│   │   ├── cleaner.py                  # Clean & transform data
│   │   ├── aggregator.py               # Create aggregations
│   │   └── validator.py                # Validate data quality
│   │
│   ├── visualization/                  # ← VISUALIZATION FOLDER
│   │   ├── __init__.py
│   │   ├── charts.py                   # Chart creation functions
│   │   ├── dashboards.py               # Dashboard layouts
│   │   ├── style.py                    # Styling & themes
│   │   └── utils.py                    # Helper functions
│   │
│   └── dashboard/
│       ├── app.py                      # Main Streamlit app
│       ├── pages/
│       │   ├── 01_overview.py
│       │   ├── 02_student_analytics.py
│       │   ├── 03_programs.py
│       │   └── 04_financial.py
│       └── components/
│           ├── kpi_cards.py
│           ├── filters.py
│           └── layouts.py
│
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_visualization.ipynb
│   └── 04_analysis.ipynb
│
└── output/
    ├── charts/                         # Exported chart images
    ├── reports/                        # Generated reports
    └── exports/                        # Data exports
```

---

## 🔧 Setup Data Folder

### Step 1: Buat Structure Awal

```bash
# Dari root project directory
mkdir -p database/data/{raw,processed,aggregated,metadata}
mkdir -p src/data
mkdir -p src/visualization
mkdir -p src/dashboard/pages
mkdir -p src/dashboard/components
mkdir -p output/{charts,reports,exports}

# Create empty __init__.py files
touch src/data/__init__.py
touch src/visualization/__init__.py
```

### Step 2: Buat Data Dictionary

```bash
# File: database/data/metadata/data_dictionary.md

# Data Dictionary - University Analytics Dashboard

## Students Table
- **student_id** (int): Unique identifier for each student
- **student_name** (varchar): Full name of student
- **email** (varchar): University email address
- **phone** (varchar): Contact phone number
- **enrollment_date** (date): Date student enrolled
- **major_id** (int): Foreign key to Programs table
- **gpa** (decimal): Current GPA (0-4.0)
- **status** (varchar): ACTIVE, GRADUATED, INACTIVE
- **created_at** (timestamp): Record creation date

## Programs Table
- **program_id** (int): Unique identifier
- **program_name** (varchar): Name of academic program
- **faculty_id** (int): Foreign key to Faculty table
- **program_type** (varchar): Undergraduate, Graduate, etc.
- **student_count** (int): Current enrollment
- **created_at** (timestamp): Record creation date

## Faculty Table
- **faculty_id** (int): Unique identifier
- **faculty_name** (varchar): Professor/instructor name
- **department** (varchar): Department assignment
- **email** (varchar): Faculty email
- **phone** (varchar): Faculty phone
- **specialization** (varchar): Area of expertise
- **created_at** (timestamp): Record creation date

## Courses Table
- **course_id** (int): Unique identifier
- **course_name** (varchar): Course title
- **course_code** (varchar): Department code
- **credits** (int): Credit hours
- **program_id** (int): Foreign key to Programs
- **faculty_id** (int): Foreign key to Faculty
- **semester** (varchar): Fall, Spring, Summer
- **capacity** (int): Max students allowed
- **created_at** (timestamp): Record creation date

## Enrollments Table
- **enrollment_id** (int): Unique identifier
- **student_id** (int): Foreign key to Students
- **course_id** (int): Foreign key to Courses
- **semester** (varchar): Enrollment semester
- **grade** (varchar): A-F or pass/fail
- **score** (decimal): Numeric score
- **status** (varchar): ENROLLED, COMPLETED, DROPPED
- **created_at** (timestamp): Record creation date
```

### Step 3: Buat Data Loader Module

```bash
# File: src/data/loader.py

"""
Data Loading Module - Load data dari berbagai sources
"""
import pandas as pd
import sqlite3
from pathlib import Path
from typing import Dict, Union

class DataLoader:
    """Load data dari CSV, Excel, atau database"""
    
    def __init__(self, data_path: str = "./database/data"):
        self.data_path = Path(data_path)
        self.raw_path = self.data_path / "raw"
        self.processed_path = self.data_path / "processed"
        self.aggregated_path = self.data_path / "aggregated"
    
    def load_raw_csv(self, filename: str) -> pd.DataFrame:
        """Load raw CSV file"""
        file_path = self.raw_path / filename
        if not file_path.exists():
            raise FileNotFoundError(f"File not found: {file_path}")
        return pd.read_csv(file_path)
    
    def load_processed_csv(self, filename: str) -> pd.DataFrame:
        """Load processed CSV file"""
        file_path = self.processed_path / filename
        if not file_path.exists():
            raise FileNotFoundError(f"File not found: {file_path}")
        return pd.read_csv(file_path)
    
    def load_aggregated(self, filename: str) -> pd.DataFrame:
        """Load aggregated data for visualization"""
        file_path = self.aggregated_path / filename
        if not file_path.exists():
            raise FileNotFoundError(f"File not found: {file_path}")
        return pd.read_csv(file_path)
    
    def load_from_db(self, query: str, db_path: str = "./database/university.db") -> pd.DataFrame:
        """Load data dari SQLite database"""
        conn = sqlite3.connect(db_path)
        df = pd.read_sql_query(query, conn)
        conn.close()
        return df
    
    def save_processed(self, df: pd.DataFrame, filename: str) -> None:
        """Save cleaned data"""
        file_path = self.processed_path / filename
        df.to_csv(file_path, index=False)
        print(f"Saved: {file_path}")
    
    def save_aggregated(self, df: pd.DataFrame, filename: str) -> None:
        """Save aggregated data"""
        file_path = self.aggregated_path / filename
        df.to_csv(file_path, index=False)
        print(f"Saved: {file_path}")
```

---

## 🧹 Data Cleaning & Preparation

### File: src/data/cleaner.py

```python
"""
Data Cleaning Module - Clean dan transform raw data
"""
import pandas as pd
import numpy as np
from typing import Tuple

class DataCleaner:
    """Clean and validate data"""
    
    def __init__(self):
        self.quality_report = {}
    
    def clean_students(self, df: pd.DataFrame) -> pd.DataFrame:
        """Clean student data"""
        df_clean = df.copy()
        
        # Remove duplicates
        df_clean = df_clean.drop_duplicates(subset=['student_id'])
        
        # Handle missing values
        df_clean['email'] = df_clean['email'].fillna('unknown@university.edu')
        df_clean['phone'] = df_clean['phone'].fillna('N/A')
        
        # Standardize GPA (0-4.0 range)
        df_clean['gpa'] = df_clean['gpa'].clip(lower=0, upper=4.0)
        
        # Convert enrollment_date to datetime
        df_clean['enrollment_date'] = pd.to_datetime(df_clean['enrollment_date'])
        
        # Validate status values
        valid_statuses = ['ACTIVE', 'GRADUATED', 'INACTIVE']
        df_clean['status'] = df_clean['status'].replace({
            'active': 'ACTIVE',
            'graduated': 'GRADUATED',
            'inactive': 'INACTIVE'
        })
        
        return df_clean
    
    def clean_programs(self, df: pd.DataFrame) -> pd.DataFrame:
        """Clean program data"""
        df_clean = df.copy()
        
        # Remove duplicates
        df_clean = df_clean.drop_duplicates(subset=['program_id'])
        
        # Remove rows with missing program_name
        df_clean = df_clean.dropna(subset=['program_name'])
        
        # Standardize program_name (title case)
        df_clean['program_name'] = df_clean['program_name'].str.title()
        
        # Ensure student_count is numeric and positive
        df_clean['student_count'] = pd.to_numeric(
            df_clean['student_count'], 
            errors='coerce'
        ).fillna(0).astype(int)
        
        return df_clean
    
    def clean_enrollments(self, df: pd.DataFrame) -> pd.DataFrame:
        """Clean enrollment data"""
        df_clean = df.copy()
        
        # Map grade values to standard A-F scale
        grade_mapping = {
            'A': 'A', 'A+': 'A', 'A-': 'A',
            'B': 'B', 'B+': 'B', 'B-': 'B',
            'C': 'C', 'C+': 'C', 'C-': 'C',
            'D': 'D', 'D+': 'D', 'D-': 'D',
            'F': 'F', 'W': 'W'  # W for withdrawn
        }
        df_clean['grade'] = df_clean['grade'].map(grade_mapping)
        
        # Ensure score is numeric (0-100 range)
        df_clean['score'] = pd.to_numeric(
            df_clean['score'], 
            errors='coerce'
        ).clip(lower=0, upper=100)
        
        return df_clean
    
    def generate_quality_report(self, df: pd.DataFrame, table_name: str) -> Dict:
        """Generate data quality report"""
        report = {
            'total_rows': len(df),
            'missing_values': df.isnull().sum().to_dict(),
            'duplicates': df.duplicated().sum(),
            'memory_usage': df.memory_usage(deep=True).sum() / 1024**2  # MB
        }
        self.quality_report[table_name] = report
        return report
```

---

## 📊 Data Visualization Design

### File: src/visualization/charts.py

```python
"""
Data Visualization Module - Create interactive charts
"""
import plotly.graph_objects as go
import plotly.express as px
import pandas as pd
from typing import Optional

class DashboardCharts:
    """Create various chart types for dashboard"""
    
    def __init__(self, theme: str = "plotly_dark"):
        self.theme = theme
    
    def enrollment_trend(self, df: pd.DataFrame) -> go.Figure:
        """Line chart - Enrollment trend over time"""
        fig = px.line(
            df,
            x='year',
            y='total_students',
            title='Student Enrollment Trend',
            labels={'year': 'Academic Year', 'total_students': 'Total Students'},
            template=self.theme
        )
        fig.update_layout(
            hovermode='x unified',
            height=400,
            showlegend=True
        )
        return fig
    
    def enrollment_by_program(self, df: pd.DataFrame) -> go.Figure:
        """Bar chart - Enrollment by program"""
        fig = px.bar(
            df,
            x='program_name',
            y='student_count',
            color='program_name',
            title='Student Enrollment by Program',
            labels={'program_name': 'Program', 'student_count': 'Students'},
            template=self.theme
        )
        fig.update_xaxes(tickangle=-45)
        fig.update_layout(height=400, showlegend=False)
        return fig
    
    def gpa_distribution(self, df: pd.DataFrame) -> go.Figure:
        """Histogram - GPA distribution"""
        fig = px.histogram(
            df,
            x='gpa',
            nbins=20,
            title='Student GPA Distribution',
            labels={'gpa': 'GPA'},
            template=self.theme
        )
        fig.update_layout(height=400, showlegend=False)
        return fig
    
    def student_status_pie(self, df: pd.DataFrame) -> go.Figure:
        """Pie chart - Student status breakdown"""
        status_counts = df['status'].value_counts()
        fig = px.pie(
            values=status_counts.values,
            names=status_counts.index,
            title='Student Status Distribution',
            template=self.theme
        )
        fig.update_layout(height=400)
        return fig
    
    def enrollment_by_semester(self, df: pd.DataFrame) -> go.Figure:
        """Grouped bar - Enrollment by semester"""
        fig = px.bar(
            df,
            x='program_name',
            y='count',
            color='semester',
            title='Enrollment by Program and Semester',
            barmode='group',
            template=self.theme
        )
        fig.update_xaxes(tickangle=-45)
        fig.update_layout(height=400)
        return fig
    
    def faculty_workload(self, df: pd.DataFrame) -> go.Figure:
        """Horizontal bar - Faculty course load"""
        fig = px.barh(
            df,
            x='course_count',
            y='faculty_name',
            color='course_count',
            title='Faculty Workload (Courses Taught)',
            labels={'course_count': 'Number of Courses'},
            template=self.theme
        )
        fig.update_layout(height=400, showlegend=False)
        return fig
```

---

## 🎨 Visualization Best Practices

### File: src/visualization/style.py

```python
"""
Styling & Theme Configuration for Visualizations
"""

class DashboardStyle:
    """Define colors, fonts, and styling"""
    
    # Color Palette (University Colors)
    COLORS = {
        'primary': '#2E8B9E',      # Teal
        'secondary': '#8B4513',     # Brown
        'accent': '#FF6B6B',        # Red
        'success': '#51CF66',       # Green
        'warning': '#FFD93D',       # Yellow
        'danger': '#FF6B6B',        # Red
        'info': '#4ECDC4',          # Cyan
        'light': '#F5F5F5',         # Light gray
        'dark': '#2C3E50'           # Dark gray
    }
    
    # Categorical Colors (for charts)
    CATEGORICAL_COLORS = [
        '#2E8B9E',  # Teal
        '#8B4513',  # Brown
        '#FF6B6B',  # Red
        '#51CF66',  # Green
        '#4ECDC4',  # Cyan
        '#FFD93D',  # Yellow
        '#FF8C42',  # Orange
        '#9D4EDD'   # Purple
    ]
    
    # Typography
    FONT_FAMILY = "Arial, sans-serif"
    FONT_SIZE_TITLE = 18
    FONT_SIZE_LABEL = 12
    FONT_SIZE_TICK = 10
    
    # Layout Configuration
    LAYOUT_CONFIG = {
        'height': 400,
        'margin': {'l': 50, 'r': 50, 'b': 50, 't': 80},
        'hovermode': 'x unified',
        'font': {'family': FONT_FAMILY}
    }
    
    @staticmethod
    def get_theme_colors(theme: str = 'light') -> dict:
        """Get colors based on theme"""
        if theme == 'dark':
            return {
                'bg': '#1a1a1a',
                'text': '#ffffff',
                'grid': '#333333'
            }
        else:
            return {
                'bg': '#ffffff',
                'text': '#2C3E50',
                'grid': '#e0e0e0'
            }
```

---

## 🚀 Implementation Langkah-Langkah

### Phase 1: Data Preparation (Minggu 1-2)

**Step 1: Collect/Generate Data**

```python
# notebooks/01_data_preparation.ipynb

import pandas as pd
import numpy as np
from src.data.loader import DataLoader

# Initialize loader
loader = DataLoader()

# Option 1: Load sample data (jika sudah ada)
students = loader.load_raw_csv('students_raw.csv')
programs = loader.load_raw_csv('programs_raw.csv')

# Option 2: Generate synthetic data
np.random.seed(42)

# Create sample students data
students = pd.DataFrame({
    'student_id': range(1, 501),
    'student_name': [f'Student_{i}' for i in range(1, 501)],
    'email': [f'student{i}@university.edu' for i in range(1, 501)],
    'enrollment_date': pd.date_range('2020-01-01', periods=500, freq='D'),
    'major_id': np.random.choice(range(1, 11), 500),
    'gpa': np.random.uniform(2.0, 4.0, 500),
    'status': np.random.choice(['ACTIVE', 'GRADUATED', 'INACTIVE'], 500)
})

# Save raw data
students.to_csv('database/data/raw/students_raw.csv', index=False)
print("✓ Sample data created")
```

**Step 2: Clean Data**

```python
from src.data.cleaner import DataCleaner

cleaner = DataCleaner()

# Clean students
students_clean = cleaner.clean_students(students)

# Generate quality report
quality = cleaner.generate_quality_report(students_clean, 'students')
print(f"Quality Report: {quality}")

# Save cleaned data
loader.save_processed(students_clean, 'students_cleaned.csv')
```

**Step 3: Create Aggregations**

```python
# Create aggregated data for visualization

# Enrollment by program
enrollment_by_program = students_clean.groupby('major_id').size().reset_index(name='student_count')
loader.save_aggregated(enrollment_by_program, 'enrollment_by_program.csv')

# GPA statistics
gpa_stats = students_clean.groupby('major_id').agg({
    'gpa': ['mean', 'min', 'max', 'std']
}).reset_index()
loader.save_aggregated(gpa_stats, 'gpa_statistics.csv')

# Status breakdown
status_breakdown = students_clean['status'].value_counts().reset_index(name='count')
loader.save_aggregated(status_breakdown, 'status_breakdown.csv')

print("✓ Aggregated data created")
```

### Phase 2: Visualization Design (Minggu 2-3)

**Step 1: Create Visualization Notebook**

```python
# notebooks/02_visualization.ipynb

import streamlit as st
from src.data.loader import DataLoader
from src.visualization.charts import DashboardCharts
from src.visualization.style import DashboardStyle

# Load data
loader = DataLoader()
enrollment_by_program = loader.load_aggregated('enrollment_by_program.csv')
students = loader.load_processed_csv('students_cleaned.csv')

# Initialize charts
charts = DashboardCharts()
style = DashboardStyle()

# Create visualizations
fig1 = charts.enrollment_by_program(enrollment_by_program)
fig2 = charts.gpa_distribution(students)
fig3 = charts.student_status_pie(students)

# Display
st.title("University Analytics Dashboard")
st.plotly_chart(fig1, use_container_width=True)
st.plotly_chart(fig2, use_container_width=True)
st.plotly_chart(fig3, use_container_width=True)
```

**Step 2: Create Streamlit Dashboard**

```python
# src/dashboard/app.py

import streamlit as st
import pandas as pd
from src.data.loader import DataLoader
from src.visualization.charts import DashboardCharts

# Page config
st.set_page_config(page_title="University Dashboard", layout="wide")

# Load data
@st.cache_data
def load_data():
    loader = DataLoader()
    return {
        'students': loader.load_processed_csv('students_cleaned.csv'),
        'programs': loader.load_aggregated('enrollment_by_program.csv'),
        'status': loader.load_aggregated('status_breakdown.csv')
    }

data = load_data()

# Title
st.title("📊 University Analytics Dashboard")

# KPI Cards
col1, col2, col3, col4 = st.columns(4)

with col1:
    st.metric("Total Students", len(data['students']), "+2.5%")

with col2:
    active = (data['students']['status'] == 'ACTIVE').sum()
    st.metric("Active Students", active, "-0.5%")

with col3:
    avg_gpa = data['students']['gpa'].mean()
    st.metric("Average GPA", f"{avg_gpa:.2f}", "+0.1")

with col4:
    programs = len(data['programs'])
    st.metric("Programs", programs, "0%")

# Charts
st.subheader("Enrollment by Program")
charts = DashboardCharts()
fig1 = charts.enrollment_by_program(data['programs'])
st.plotly_chart(fig1, use_container_width=True)

st.subheader("Student Status Distribution")
fig2 = charts.student_status_pie(data['status'])
st.plotly_chart(fig2, use_container_width=True)
```

### Phase 3: Testing & Optimization (Minggu 3-4)

```python
# tests/test_data_quality.py

import pytest
import pandas as pd
from src.data.cleaner import DataCleaner

class TestDataQuality:
    """Test data quality after cleaning"""
    
    @pytest.fixture
    def sample_data(self):
        return pd.DataFrame({
            'student_id': [1, 2, 3],
            'gpa': [3.5, 3.8, 2.1]
        })
    
    def test_gpa_range(self, sample_data):
        """Test GPA is within valid range"""
        cleaner = DataCleaner()
        cleaned = cleaner.clean_students(sample_data)
        assert (cleaned['gpa'] >= 0).all()
        assert (cleaned['gpa'] <= 4.0).all()
    
    def test_no_duplicates(self, sample_data):
        """Test no duplicate student IDs"""
        cleaner = DataCleaner()
        cleaned = cleaner.clean_students(sample_data)
        assert len(cleaned) == len(cleaned.drop_duplicates(subset=['student_id']))
```

---

## ✨ Best Practices

### 1. Data Organization
```
✅ Separate raw, processed, and aggregated data
✅ Document all transformations
✅ Keep data dictionary updated
✅ Version control for critical datasets
```

### 2. Code Organization
```
✅ Separate concerns (data, visualization, dashboard)
✅ Reusable functions and classes
✅ Clear naming conventions
✅ Comprehensive comments
```

### 3. Visualization Design
```
✅ Choose appropriate chart types
✅ Use consistent color palettes
✅ Make interactive (filters, drill-down)
✅ Add context (titles, labels, legends)
✅ Optimize for readability
```

### 4. Performance
```
✅ Cache processed data
✅ Use aggregated data for visualizations
✅ Limit data points displayed
✅ Optimize database queries
```

### 5. Documentation
```
✅ Data dictionary for all tables
✅ Data quality reports
✅ ETL documentation
✅ Chart descriptions
```

---

## 📊 Command Reference

```bash
# Data operations
python scripts/generate_sample_data.py      # Generate sample data
python scripts/clean_data.py                # Run data cleaning
python scripts/aggregate_data.py            # Create aggregations

# Visualization
jupyter notebook                            # Open Jupyter for exploration
streamlit run src/dashboard/app.py          # Run dashboard

# Testing
pytest tests/                               # Run all tests
pytest tests/test_data_quality.py           # Test specific module

# Database
sqlite3 database/university.db              # Open database
sqlite3 database/university.db < database/schemas/schema.sql  # Initialize DB
```

---

## 🎯 Quick Start Checklist

- [ ] Create data folder structure
- [ ] Create data dictionary
- [ ] Generate/collect initial data
- [ ] Run data cleaning scripts
- [ ] Create aggregations
- [ ] Build visualization functions
- [ ] Create Streamlit dashboard
- [ ] Test all components
- [ ] Document everything
- [ ] Deploy dashboard

---

**Next Step**: Follow Phase 1 untuk memulai data preparation Anda! 🚀
