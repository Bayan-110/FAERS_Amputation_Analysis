# faers-canagliflozin-analysis
# FAERS-Based SGLT-2 Inhibitor Amputation Risk Signal Mining

A real-world pharmacovigilance analysis comparing amputation risk signals between Canagliflozin and Dapagliflozin using FDA AEMS data.

## Project Overview

In 2017, the FDA issued a Black Box Warning for Canagliflozin due to increased risk of lower limb amputation. This project aims to:
- **Validate** the amputation signal using real-world adverse event data
- **Compare** signal characteristics between Canagliflozin and Dapagliflozin
- **Provide** data-driven evidence for clinical decision-making

## Key Findings

### 1. Canagliflozin: Amputation is the Strongest Signal
Among all adverse events associated with Canagliflozin, amputation showed the highest signal:
- **ROR: 404.88** (95% CI: 351.36 - 466.55)
- Nearly **3× stronger** than the second-ranked signal (Osteomyelitis, ROR=138.34)

### 2. Cross-Drug Comparison: Same Signal, Different Scale
| Metric | Canagliflozin | Dapagliflozin |
|--------|--------------|---------------|
| Amputation-related Reports | 332 | 17 |
| Amputation ROR | 404.88 | 422.22 |
| Drug-AE Combinations | 1,152 | 64 |

**Key Insight**: Both drugs show extremely high amputation signal strength, but the reporting frequency differs by nearly **20×**, suggesting a significant intra-class safety difference.

### 3. Subtype Analysis
Canagliflozin-associated amputation events are highly correlated with:
- Gangrene (ROR=66.7)
- Diabetic foot (ROR=50.1)
- Osteomyelitis (ROR=138.3)

## Data Source
- **Database**: FDA Adverse Event Monitoring System (AEMS)
- **Access Method**: OpenFDA API
- **Sample Size**: 1,230 amputation-related individual case safety reports
- **Analysis Period**: Through 2026

## Technical Pipeline

​```mermaid
flowchart LR
    A[OpenFDA API] --> B[Python Data Fetching]
    B --> C[JSON Parsing & Cleaning]
    C --> D[Pandas DataFrame]
    D --> E[ROR Signal Detection]
    E --> F[Matplotlib Visualization]
    F --> G[Final Report PDF]
​```

## Methodology

### Signal Detection: Reporting Odds Ratio (ROR)

ROR = (a/b) / (c/d), where:
- **a**: Number of reports with the target AE for the target drug
- **b**: Number of reports with other AEs for the target drug
- **c**: Number of reports with the target AE for all other drugs
- **d**: Number of reports with other AEs for all other drugs

**Signal Threshold**: ROR > 2 with 95% CI lower bound > 1

## Repository Structure

​```
FAERS_Amputation_Analysis/
├── data/
│   ├── canagliflozin_faers.json         # Raw Canagliflozin data (5,000 records)
│   ├── amputation_faers.json            # Amputation-specific reports (1,230 records)
│   ├── canagliflozin_ror_signals.csv    # ROR analysis results
│   └── dapagliflozin_ror_signals.csv    # Comparative analysis results
├── notebooks/
│   └── faers_analysis.ipynb             # Complete analysis notebook
├── figures/
│   ├── canagliflozin_signal_charts.png  # Top 15 AE signal ranking
│   └── final_comparison_chart.png       # Cross-drug comparison
├── report/
│   └── FAERS_Analysis_Report.pdf        # Final 10-page report
└── README.md
​```

## Tools & Technologies

- **Language**: Python 3.9+
- **Libraries**: Pandas, NumPy, Matplotlib, Requests, JSON
- **External API**: OpenFDA Drug Adverse Event API
- **Methodology**: Reporting Odds Ratio (ROR) Disproportionality Analysis

## How to Reproduce

### 1. Clone the Repository
​```bash
git clone https://github.com/yourusername/FAERS_Amputation_Analysis.git
cd FAERS_Amputation_Analysis
​```

### 2. Install Dependencies
​```bash
pip install pandas numpy matplotlib requests jupyter
​```

### 3. Fetch Data from OpenFDA
​```python
python fetch_data.py
​```

### 4. Run Analysis
Open `notebooks/faers_analysis.ipynb` in Jupyter and run all cells.

## Limitations

- FAERS data cannot be used to calculate incidence rates
- Spontaneous reporting system has inherent reporting bias
- Causality cannot be established from disproportionality analysis alone
- Results should be interpreted alongside clinical trials and other evidence

## References

1. FDA Adverse Event Monitoring System (AEMS) Public Dashboard
2. OpenFDA API Documentation
3. van Puijenbroek EP, et al. "A comparison of measures of disproportionality for signal detection in spontaneous reporting systems." Pharmacoepidemiology and Drug Safety, 2002.

## Author

Bayan | ba__yan@outlook.com

## License

This project is for educational and research purposes.
