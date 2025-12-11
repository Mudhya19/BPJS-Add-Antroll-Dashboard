# Quick Reference Guide - University Analytics Dashboard

## 🚀 Quick Start (30 seconds)

```bash
# 1. Navigate to project
cd university_dashboard

# 2. Run setup
chmod +x setup.sh && ./setup.sh

# 3. Activate environment
source .venv/bin/activate

# 4. Run dashboard
./run.sh
```

Open: **http://localhost:8501**

---

## 📁 Generated Project Structure Overview

```
university_dashboard/
├── .venv/                   ← Virtual environment
├── src/                     ← Source code
│   ├── dashboard/app.py     ← Main app
│   ├── data/loader.py       ← Data utilities
│   └── utils/               ← Helper functions
├── notebooks/               ← Jupyter notebooks
├── docs/                    ← Documentation
├── database/                ← Database & data
│   ├── data/                ← CSV files
│   └── schemas/             ← SQL schemas
├── images/                  ← Screenshots & mockups
├── output/                  ← Reports & exports
├── tests/                   ← Unit tests
├── config/                  ← Configuration
├── scripts/                 ← Helper scripts
├── requirements.txt         ← Dependencies
├── .env                     ← Environment vars
├── .gitignore               ← Git ignore
├── setup.sh                 ← Setup script
├── run.sh                   ← Run script
└── README.md                ← Documentation
```

---

## 📦 Key Packages Installed

| Package | Version | Purpose |
|---------|---------|---------|
| **streamlit** | 1.28.1 | Web framework |
| **pandas** | 2.1.1 | Data processing |
| **plotly** | 5.18.0 | Interactive charts |
| **sqlalchemy** | 2.0.23 | Database ORM |
| **jupyter** | 1.0.0 | Notebooks |
| **pytest** | 7.4.3 | Testing |
| **scikit-learn** | 1.3.2 | ML library |

[Full list in requirements.txt]

---

## 🎯 Development Workflow

### 1. **Start Development**
```bash
source .venv/bin/activate
jupyter notebook
# or
streamlit run src/dashboard/app.py
```

### 2. **Write Code**
- Edit files in `src/` directory
- Add functions to `src/data/loader.py`
- Create new pages in `src/dashboard/app.py`

### 3. **Test Code**
```bash
pytest tests/
pytest --cov=src tests/
```

### 4. **Format Code**
```bash
black src/
flake8 src/
```

### 5. **Version Control**
```bash
git add .
git commit -m "Add feature X"
git push origin main
```

---

## 📊 Dashboard Development Checklist

### Phase 1: Planning
- [ ] Define user personas
- [ ] List KPIs and metrics
- [ ] Design wireframes/mockups
- [ ] Identify data sources
- [ ] Document requirements

### Phase 2: Data Preparation
- [ ] Load/import data
- [ ] Clean and validate data
- [ ] Create data samples
- [ ] Build data pipeline
- [ ] Document data schema

### Phase 3: Development
- [ ] Setup base pages
- [ ] Create visualizations
- [ ] Add filters and interactivity
- [ ] Implement responsive design
- [ ] Add loading states

### Phase 4: Testing
- [ ] Unit tests
- [ ] Integration tests
- [ ] User acceptance tests
- [ ] Performance testing
- [ ] Cross-browser testing

### Phase 5: Deployment
- [ ] Code review
- [ ] Documentation
- [ ] Deploy to server
- [ ] Monitor performance
- [ ] User training

---

## 🔧 Common Commands

### Environment Management
```bash
# Activate
source .venv/bin/activate          # Linux/macOS
.venv\Scripts\activate.bat         # Windows

# Deactivate
deactivate

# Reinstall venv
rm -rf .venv
python3 -m venv .venv
```

### Package Management
```bash
# Install single package
pip install package_name

# Update all packages
pip install --upgrade -r requirements.txt

# List packages
pip list

# Generate requirements
pip freeze > requirements.txt
```

### Run Applications
```bash
# Run dashboard
streamlit run src/dashboard/app.py

# Run tests
pytest
pytest -v
pytest --cov=src

# Start notebook
jupyter notebook
jupyter lab
```

### Data Operations
```bash
# Generate sample data
python scripts/generate_sample_data.py

# Initialize database
python scripts/init_database.py

# Import data
python scripts/data_import.py
```

### Code Quality
```bash
# Format code
black src/

# Check style
flake8 src/
pylint src/

# Check complexity
radon cc src/
```

---

## 🐛 Troubleshooting Quick Fixes

| Problem | Solution |
|---------|----------|
| `Python not found` | Install Python 3.9+ from python.org |
| `Permission denied` | `chmod +x setup.sh` |
| `venv not activating` | `rm -rf .venv && python3 -m venv .venv` |
| `pip install fails` | `pip install --upgrade pip` |
| `Port 8501 in use` | `streamlit run app.py --server.port 8502` |
| `ModuleNotFoundError` | Ensure venv is activated |
| `Database locked` | `rm database/university.db` |

---

## 📚 File Reference

### Configuration Files
- **`.env`** - Environment variables (API keys, paths, etc.)
- **`config/config.py`** - Python configuration module
- **`requirements.txt`** - Python dependencies
- **`.gitignore`** - Files to ignore in Git

### Source Code
- **`src/dashboard/app.py`** - Main Streamlit application
- **`src/data/loader.py`** - Data loading utilities
- **`src/utils/`** - Helper functions and utilities

### Database
- **`database/schemas/schema.sql`** - Database schema
- **`database/data/`** - Data files (CSV, Excel)
- **`database/university.db`** - SQLite database (created at runtime)

### Documentation
- **`README.md`** - Project overview
- **`docs/CONTRIBUTING.md`** - Contributing guidelines
- **`SETUP_SUMMARY.txt`** - Setup summary
- **`PANDUAN_SETUP.md`** - Detailed setup guide (Indonesian)

### Notebooks
- **`notebooks/01_data_exploration.ipynb`** - Data exploration
- **`notebooks/02_data_cleaning.ipynb`** - Data cleaning
- **`notebooks/03_visualization.ipynb`** - Visualization
- **`notebooks/04_analysis.ipynb`** - Statistical analysis

### Scripts
- **`setup.sh`** - Automated setup
- **`run.sh`** - Run dashboard
- **`scripts/generate_sample_data.py`** - Generate sample data
- **`scripts/init_database.py`** - Initialize database
- **`scripts/data_import.py`** - Import data

### Tests
- **`tests/test_data_loader.py`** - Data loader tests
- **`tests/test_app.py`** - App tests
- **`pytest.ini`** - Pytest configuration

---

## 🎨 Customization Tips

### Adding New Dashboard Page

Edit `src/dashboard/app.py`:
```python
# Add to navigation
page = st.sidebar.radio(
    "Select Page:",
    ["Home", "Overview", "Your New Page"]
)

# Add handler
if page == "Your New Page":
    st.title("Your New Page")
    # Add your content here
```

### Changing Database

Edit `.env`:
```
DB_TYPE=postgresql    # or mysql, mongodb, etc
DB_CONNECTION_URL=postgresql://user:pass@host/db
```

### Adding New Dependencies

```bash
# Install
pip install new_package

# Update requirements
pip freeze > requirements.txt

# Commit changes
git add requirements.txt
git commit -m "Add new_package"
```

### Customizing Colors & Styling

Edit `src/dashboard/app.py`:
```python
st.set_page_config(
    page_title="My Dashboard",
    page_icon="🎓",
    layout="wide",  # or "centered"
    initial_sidebar_state="expanded"  # or "collapsed"
)
```

---

## 🔐 Security Tips

1. **Never commit .env** - Keep secrets in environment variables
2. **Use secrets manager** - For production API keys
3. **Validate input** - Always validate user inputs
4. **Sanitize data** - Clean data before display
5. **HTTPS only** - Use HTTPS in production
6. **Rate limiting** - Implement rate limits on APIs
7. **Error handling** - Don't expose stack traces to users

---

## 📈 Performance Tips

1. **Cache data** - Use `@st.cache` decorator
2. **Lazy loading** - Load data only when needed
3. **Pagination** - Paginate large datasets
4. **Indexing** - Add database indexes
5. **Compress images** - Optimize image sizes
6. **Minify CSS/JS** - Minimize asset sizes
7. **CDN** - Use CDN for static files

---

## 🚀 Deployment Options

### Local Development
```bash
streamlit run src/dashboard/app.py
```

### Streamlit Cloud
```bash
streamlit run src/dashboard/app.py --logger.level=debug
```

### Docker (Optional)
```bash
docker build -t university-dashboard .
docker run -p 8501:8501 university-dashboard
```

### Heroku
```bash
git push heroku main
heroku logs --tail
```

---

## 📞 Support & Resources

- **Streamlit Docs**: https://docs.streamlit.io
- **Pandas Docs**: https://pandas.pydata.org
- **Plotly Docs**: https://plotly.com/python
- **Stack Overflow**: Tag with [streamlit], [pandas], [python]
- **GitHub Issues**: Report bugs on project GitHub

---

## 📝 Notes

- Keep `.env` file **private** - add to `.gitignore`
- Update `requirements.txt` when adding packages
- Write tests for new features
- Document complex functions with docstrings
- Commit frequently with meaningful messages
- Use branches for new features
- Review code before merging

---

## 🎓 Project Timeline (Suggested)

| Week | Task |
|------|------|
| **W1** | Setup project, explore data |
| **W2** | Design dashboard, create mockups |
| **W3** | Build data pipeline, load data |
| **W4** | Create visualizations, add filters |
| **W5** | Test, debug, optimize |
| **W6** | Documentation, final review |
| **W7** | Presentation preparation |
| **W8** | Presentation & submission |

---

## ✅ Pre-Submission Checklist

- [ ] All code tested and working
- [ ] Documentation complete
- [ ] README.md updated
- [ ] Code formatted (black, flake8)
- [ ] No hardcoded secrets/API keys
- [ ] No unused imports
- [ ] Comments for complex logic
- [ ] Database schema documented
- [ ] Sample data included
- [ ] GitHub repository setup
- [ ] Presentation slides ready
- [ ] Evaluation document prepared

---

**Version**: 1.0.0  
**Last Updated**: December 2025  
**Course**: Data Insight - Magister Teknik Informatika