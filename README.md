# AI Exposure and Labor Market Displacement Across U.S. Occupations

**An independent research project exploring how AI exposure differs across U.S. occupations and what this means for jobs, wages, and at-risk groups.**

##

## Project Origin

This project grew out of research questions from my ECO483 (Health and Economic Inequality) course in Winter 2026 at the University of Toronto, where I studied the relationship between Income Inequality, Social Capital, and Mental Health Distress in U.S. counties. That work sharpened my interest in how structural economic forces shape labor market outcomes and downstream well-being.

The growing discussion around AI and jobs in early 2026 gave this project both motivation and context. The Federal Reserve noted AI-related hiring caution in its January 2026 FOMC minutes, and the Peterson Institute for International Economics (PIIE) published a major review in March 2026 characterizing research on AI's labor market effects as "still in the first inning" (Kolko, 2026).

##

## Research Questions

1. **Occupational mapping:** Which occupations, industries, and metro areas face the highest AI displacement risk?
2. **Wage and skill correlates:** How does AI exposure relate to current wage levels, employment concentration, and education requirements?
3. **Demographic vulnerability:** Are there demographic patterns (e.g., gender-dominated occupations) where AI exposure is unevenly concentrated?
4. **Employment dynamics:** Using a 2019–2024 panel, have high-exposure occupations already begun to diverge from low-exposure occupations in employment and wage growth?

##

## Key Findings

- **AI exposure is concentrated in cognitive, high-wage occupations.** The correlation between AIOE and log annual wages is r = 0.54 (p < 0.001), confirming that, unlike past automation waves, AI mainly affects white-collar, knowledge-heavy work (financial analysts, management analysts, accountants, market researchers).
- **Education increases exposure.** Occupations requiring a bachelor's degree or higher have much higher AIOE scores than those requiring a high school diploma or less (r = 0.68 between AIOE and education level, p < 0.001).
- **Gender gap in exposure.** Female-dominated occupation groups (office/administrative, education, healthcare support) have much higher mean AI exposure (AIOE = 0.54) than male-dominated groups (construction, transportation, production; AIOE = −0.71), t = −16.05, p < 0.001.
- **Geographic patterns.** Washington D.C., Massachusetts, New York, Virginia, and Connecticut are the most AI-exposed states, reflecting their large share of knowledge-economy jobs.
- **Regression results hold up.** AIOE remains a significant predictor of wages (p < 0.001) even after controlling for education, occupation group, and employment size (R² = 0.64). The bivariate model alone explains 29.4% of wage variation.
- **K-means clustering identifies four risk tiers:** Low Risk (219 occupations), Moderate Risk (150), Elevated Risk (144), and High Risk (157), offering a data-driven framework for targeted policy responses.
- **Difference-in-differences (2019–2024) reveals employment growth, not decline, in high-AIOE occupations.** The DiD interaction on log employment is positive and significant (β = 0.052, p < 0.001), while wage growth was meaningfully slower in high-AIOE occupations (DiD interaction β = −0.029, p < 0.001). This pattern is consistent with AI-augmented labor supply expanding effective cognitive work and compressing skill premiums rather than producing wholesale displacement.
- **Within-group heterogeneity is stark.** Routine cognitive roles contracted sharply (credit authorizers −55%, telemarketers −51%, switchboard operators −48%), while managerial and research roles grew (industrial-organizational psychologists +67%, epidemiologists +55%, sales managers +50%, computer and information systems managers +49%). This divergence supports task-level distinctions between substitution and augmentation.

##

All data files are publicly available and were downloaded directly from the following sources:

## Data Sources

### AI Occupational Exposure Index (AIOE)
- **Source:** Felten et al. (2021) - GitHub
- **Download path:** Click `AIOE_DataAppendix.xlsx` → download raw file
- **File used:** `AIOE_DataAppendix.xlsx` (Appendix A: 774 occupations)

### Occupational Employment & Wage Statistics (OEWS)
- **Source:** BLS, May 2024
- **Download path:** May 2024 → National (XLSX) → unzip
- **File used:** `national_M2024_dl.xlsx` (831 detailed occupations, 32 columns)

### OEWS May 2019 (for DiD panel)
- **Source:** BLS, May 2019
- **Download path:** May 2019 → National (XLSX) → unzip
- **File used:** `national_M2019_dl.xlsx` (789 detailed occupations, 30 columns)

### O*NET Database 30.2
- **Source:** O*NET Resource Center
- **Download path:** All Files → Excel → unzip
- **Files used:** `Education, Training, and Experience.xlsx`, `Job Zones.xlsx`

### AI Geographic Exposure (AIGE)
- **Source:** Felten et al. (2021) - GitHub
- **Download path:** Same file as AIOE above
- **File used:** `AIOE_DataAppendix.xlsx` (Appendix C: 3,271 counties/states)

### AI Industry Exposure (AIIE)
- **Source:** Felten et al. (2021) - GitHub
- **Download path:** Same file as AIOE above
- **File used:** `AIOE_DataAppendix.xlsx` (Appendix B: 250 4-digit NAICS industries)

## How to Run

### Prerequisites

- Python 3.9+
- Jupyter Notebook or JupyterLab

### Installation

```bash
# Clone the repository
git clone https://github.com/rx-stack0001/ai-labor-market-displacement.git
cd ai-labor-market-displacement

# Install dependencies
pip install pandas numpy matplotlib seaborn scipy scikit-learn statsmodels openpyxl xlrd nbformat jupyter

# Launch the notebook
jupyter notebook AI_Labour_Market_Jupyter.ipynb
```

### Dependencies

- **pandas** (>=1.5): Data manipulation and merging
- **numpy** (>=1.23): Numerical computation
- **matplotlib** (>=3.6): Visualization
- **seaborn** (>=0.12): Statistical graphics
- **scipy** (>=1.9): Statistical tests
- **scikit-learn** (>=1.2): K-means clustering
- **statsmodels** (>=0.13): OLS regression and clustered standard errors
- **openpyxl** (>=3.0): Excel file reading

##

## Methodology

The analysis follows a structured, step-by-step model-building approach:

1. **Data merging:** AIOE, OEWS (May 2024 and May 2019), and O\*NET 30.2 datasets are joined on six-digit SOC codes, producing 673 matched occupations for the cross-sectional sample (659 with complete education data) and a balanced panel of 661 occupations observed in both 2019 and 2024.
2. **Exploratory analysis:** Distributions, rankings, and cross-tabulations describe the AI exposure landscape across occupations, occupation groups, education levels, states, and industries.
3. **Bivariate regression (Model 1):** Log(annual wage) regressed on AIOE alone (R² = 0.294).
4. **Multivariate regression (Model 2):** Controls for education level, occupation group fixed effects, and log employment are added (R² = 0.640). All cross-sectional models use heteroskedasticity-robust (HC1) standard errors.
5. **Interaction model (Model 3):** An AIOE × graduate-education interaction tests whether the wage effect of AI exposure attenuates at the top of the education distribution (R² = 0.643).
6. **K-means clustering:** Occupations are sorted into four risk tiers based on AIOE, log wages, and log employment; k = 4 is supported by silhouette analysis.
7. **Demographic analysis:** Gender composition of occupation groups is tested for systematic differences in AI exposure via two-sample t-tests.
8. **Difference-in-differences (DiD):** A two-period panel (2019–2024) tests whether high-AIOE occupations experienced differential employment or wage changes. First-difference regressions on Δlog(Y) and a formal panel DiD specification (Y_it = α + β₁·AIOE_i + β₂·Post_t + β₃·(AIOE_i × Post_t) + ε_it) with occupation-clustered standard errors are estimated. Tercile comparisons and t-tests provide robustness checks, and a winners-vs.-losers decomposition of high-AIOE occupations highlights within-group heterogeneity.

##

## References

- Acemoglu, D., & Restrepo, P. (2020). Robots and jobs: Evidence from US labor markets. *Journal of Political Economy, 128*(6), 2188–2244.
- Brynjolfsson, E., & Mitchell, T. (2017). What can machine learning do? Workforce implications. *Science, 358*(6370), 1530–1534.
- Brynjolfsson, E., Chandar, B., & Chen, J. (2025). Canaries in the coal mine: Six facts about the recent employment effects of artificial intelligence. *Stanford Digital Economy Lab Working Paper.*
- Eckhardt, S., & Goldschlag, N. (2025). AI and jobs: The final word? *Economic Innovation Group.*
- Eloundou, T., Manning, S., Mishkin, P., & Rock, D. (2023). GPTs are GPTs: An early look at the labor market impact potential of large language models. *arXiv:2303.10130.*
- Felten, E., Raj, M., & Seamans, R. (2021). Occupational, industry, and geographic exposure to artificial intelligence: A novel dataset and its potential uses. *Strategic Management Journal, 42*(12), 2195–2217.
- Frank, M. R., et al. (2026). Toward understanding the impact of artificial intelligence on labor. *arXiv:2601.02554.*
- Iscenko, Z., & Millet, T. (2026). Job postings and AI exposure: Disentangling technology from macroeconomic trends. *Economic Innovation Group Working Paper.*
- Kolko, J. (2026). Research on AI and the labor market is still in the first inning. *The Hamilton Project, Brookings Institution / Peterson Institute for International Economics.*
- Manning, S., & Aguirre, T. (2026). How adaptable are American workers to AI-induced job displacement? *NBER Working Paper No. 34705.*
- Massenkoff, M., & McCrory, P. (2026). Labor market impacts of AI: A new measure and early evidence. *Anthropic Research.*
- Webb, M. (2020). The impact of artificial intelligence on the labor market. *Working Paper, Stanford University.*

##

## Generative AI Disclosure

Claude Opus 4.6 was used for Python coding support, including fixing syntax errors and bugs, explaining error messages, and helping ensure the code ran properly. Grammarly was used for grammar and style correction. All empirical decisions, model specifications, interpretations of results, and claims in this report are my own.

##

## License

This project is released for academic and educational purposes. Data sources keep their original licenses. The AIOE dataset is available under the Creative Commons Attribution License via [Felten et al. (2021)](https://github.com/AIOE-Data/AIOE).
