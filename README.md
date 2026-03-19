# AI CTD Analysis

**AI-powered Cycle Time Deviation and Maintenance Effectiveness Analysis for Manufacturing Operations**

## Overview

This repository contains a comprehensive Python-based analysis tool designed to evaluate maintenance effectiveness through cycle time deviation analysis. The tool features an interactive Streamlit web interface, real-time Snowflake data integration, and advanced statistical analysis with adaptive algorithms for manufacturing equipment monitoring.

## 🚀 Features

- 🌐 **Interactive Streamlit Web Interface** - User-friendly dashboard for data analysis
- 🔄 **Real-time Snowflake Integration** - Direct database connectivity with environment-based authentication
- 📊 **Enhanced Maintenance Effectiveness Analysis** - Statistical significance testing with adaptive window sizing
- 🎯 **Adaptive Window Algorithm** - Automatically adjusts analysis windows (30-90 days) based on data availability
- 📈 **Advanced Visualizations** - 4-panel effectiveness dashboard with color-coded maintenance classifications
- 📄 **Automated PDF Reports** - Comprehensive reports with actionable recommendations
- 🔍 **Data Quality Assessment** - Real-time validation and completeness analysis
- ⚡ **Intelligent Error Handling** - Robust processing with clear user feedback

## 📁 File Structure

```
ai_ctd_analysis/
├── streamlit_ctd_analysis.py    # Main Streamlit web interface
├── ctd_analysis.py              # Core analysis engine with adaptive algorithms
├── debug_data.py                # Data validation and debugging utilities
└── README.md                    # This file
```

## 🛠️ Requirements

### Python Environment
- Python 3.11 or later
- Streamlit-compatible environment

### Dependencies
```bash
pip install streamlit pandas numpy matplotlib reportlab scipy scikit-learn snowflake-snowpark-python python-dotenv
```

### Environment Variables
Create a `.env` file with your Snowflake credentials:
```env
SNOWFLAKE_ACCOUNT=your_account.region
SNOWFLAKE_USER=your_username
SNOWFLAKE_PASSWORD=your_password
SNOWFLAKE_ROLE=your_role
SNOWFLAKE_WAREHOUSE=your_warehouse
```

## 📊 Data Requirements

### Snowflake Table Structure
The tool expects data from: `MMS.{schema}.AI_CTD_MAINTAINENCE_TABLE`

#### Required Columns (Core Analysis)
- `EQUIPMENT_CODE` - Unique equipment identifier
- `LOCAL_SHOT_TIME` - Timestamp of each cycle measurement
- `CT` - Cycle time in seconds
- `DURING_MAINTENANCE` - Binary maintenance indicator (0/1)

#### Optional Columns (Enhanced Analysis)
- `WORK_ORDER_ID` - Maintenance work order identifier
- `MAINTENANCE_AT` - Maintenance execution timestamp
- `WO_START` / `WO_END` - Maintenance window boundaries
- `MAINTENANCE_CREATED_AT` - Maintenance creation timestamp
- `MAINTENANCE_STARTED_ON` - Maintenance start timestamp
- `MAINTENANCE_COMPLETED_ON` - Maintenance completion timestamp

## 🚀 Usage

### 1. Launch Streamlit Application
```bash
streamlit run streamlit_ctd_analysis.py
```

### 2. Web Interface Workflow
1. **Connect to Snowflake** - Enter schema name and equipment code
2. **Data Quality Review** - Assess data completeness and availability
3. **Equipment Selection** - Choose specific equipment (if multiple available)
4. **Run Analysis** - Execute maintenance effectiveness analysis
5. **Review Results** - Interactive visualizations and metrics
6. **Download Report** - PDF report with detailed findings

### 3. Direct Analysis (Advanced Users)
```python
from ctd_analysis import EnhancedMaintenanceAnalyzer

# Initialize analyzer
analyzer = EnhancedMaintenanceAnalyzer('your_data_file.csv')

# Run complete analysis
results = analyzer.run_enhanced_analysis()
```

## 📈 Analysis Methodology

### Adaptive Window Strategy
- **Primary Window**: 30 days before/after maintenance
- **Fallback Windows**: 45, 60, 90 days if insufficient data
- **Minimum Requirement**: 50 shots per window for statistical significance

### Effectiveness Classification
- **Effective (≥60 points)**: Significant improvement in stability and anomaly reduction
- **Neutral (30-59 points)**: Mixed or minimal impact
- **Ineffective (<30 points)**: No improvement or degradation

### Statistical Analysis
- **Mann-Whitney U Test**: Non-parametric comparison of cycle time distributions
- **Chi-square Test**: Anomaly rate significance testing
- **Threshold Calculation**: Mode-based adaptive anomaly detection

## 📊 Output

### Streamlit Dashboard
- **Data Quality Metrics** - Real-time completeness assessment
- **Equipment Summary** - Total records, maintenance coverage, work orders
- **Interactive Visualizations** - 4-panel effectiveness analysis
- **Downloadable Reports** - PDF with detailed findings

### Generated Files
- `enhanced_maintenance_analysis_{EQUIPMENT_CODE}.png` - Visualization dashboard
- `report_outputs/Enhanced_Maintenance_Report_{EQUIPMENT_CODE}_{DATE}.pdf` - Comprehensive report

### Console Output
```
Detected 15 maintenance events by MAINTENANCE_AT
Analyzed 12 maintenance events for effectiveness

Maintenance Effectiveness Summary:
  Effective: 3
  Neutral: 4  
  Ineffective: 5
  Average Score: 42.3/100

Window sizes used: [30, 45, 60] days
```

## 🔧 Advanced Configuration

### Custom Thresholds
Modify in `ctd_analysis.py`:
```python
# Adjust anomaly detection sensitivity
self.ct_threshold = std_from_mode / 3  # Default: /3

# Change minimum shots requirement  
min_shots = 50  # Default: 50

# Modify window sizes
window_sizes = [30, 45, 60, 90]  # Default progression
```

### Database Configuration
Update connection in `streamlit_ctd_analysis.py`:
```python
# Modify table reference
query = f"SELECT * FROM MMS.{schema_name}.AI_CTD_MAINTAINENCE_TABLE"
```

## 🚨 Troubleshooting

### Common Issues
1. **No Maintenance Data Found**
   - Verify `WORK_ORDER_ID` and `MAINTENANCE_AT` columns have values
   - Check data date ranges

2. **Insufficient Data for Analysis**
   - Tool automatically tries larger windows (45, 60, 90 days)
   - Minimum 50 shots required per window

3. **Snowflake Connection Issues**
   - Verify environment variables in `.env` file
   - Check network connectivity and credentials

## 📝 Notes

- The tool prioritizes `MAINTENANCE_AT` timestamps for precise analysis timing
- Analysis windows automatically adapt based on data availability
- Statistical significance testing ensures reliable effectiveness classifications
- All maintenance events are analyzed individually (no merging of overlapping periods)

## 🏢 eMoldino Integration

This tool is designed for eMoldino's manufacturing analytics pipeline, supporting:
- Multi-equipment analysis across production lines
- Integration with existing MMS database structure
- Scalable analysis for large datasets
- Enterprise-grade error handling and reporting

## 📄 License

This project is developed for eMoldino's internal manufacturing analytics. Usage is subject to company policies and data governance guidelines.

---

**Developed with ❤️ for Manufacturing Excellence** 