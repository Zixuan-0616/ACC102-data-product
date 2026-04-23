# WRDS Financial Data Analysis: Firm Size and Stock Volatility

## Project Purpose
This project analyzes the relationship between firm size (market capitalization) and stock return volatility using historical CRSP data from WRDS. The target audience includes equity research analysts and finance students interested in empirical asset pricing.

**Analytical Problem**: Do smaller firms (small market capitalization) exhibit higher stock return volatility than larger firms?

**Hypothesis**: Small-cap firms have higher daily volatility due to lower liquidity, higher information asymmetry, and greater business risk.

## Data Source
- **Platform**: Wharton Research Data Services (WRDS)
- **Database**: CRSP Daily Stock File (`crsp.dsf`)
- **Time Period**: January 1, 2024 – December 31, 2024
- **Access Date**: April 21, 2026

## Key Variables
| Variable | Description |
|----------|-------------|
| permno | Permanent company identifier |
| date | Trading date |
| ret | Daily stock return (decimal, e.g., 0.01 = 1%) |
| prc | Price per share |
| shrout | Shares outstanding (in thousands) |

**Important Note**: The CRSP field `vol` represents **trading volume**, not price volatility. All volatility calculations in this analysis are derived from the `ret` (return) column.

## Methodology

### 1. Market Capitalization Calculation
Market cap is calculated as: `mktcap = |prc| × (shrout × 1000)`

### 2. Firm Size Classification
To ensure stable classification (rather than daily fluctuations), each firm is classified based on its **average market cap across 2024**:
- **Small Cap**: Average market cap ≤ median firm-level average market cap
- **Large Cap**: Average market cap > median firm-level average market cap

This approach aligns with standard empirical finance practices (e.g., Fama-French portfolio sorts).

### 3. Volatility Calculation
- **20-day rolling standard deviation** of daily returns
- **Minimum 5 observations** per rolling window (`min_periods=5`)
- Outliers removed where `rolling_vol > 1.0` (daily std dev exceeding 100%)

### 4. Analysis Outputs
- Average volatility by size group
- Bar chart comparison
- Time series visualization for an individual firm
- Summary statistics table

## Key Findings

| Size Group | Average 20-Day Rolling Volatility |
|------------|-----------------------------------|
| Small Cap  | 0.0314 (3.14% daily std dev) |
| Large Cap  | 0.0206 (2.06% daily std dev) |

**Small-cap volatility is approximately 52% higher than large-cap volatility.**

**Business Implication**: Equity analysts should demand higher expected returns from small-cap allocations to compensate for increased volatility risk. The size premium observed in financial markets is partially explained by this elevated volatility.

## Repository Contents

| File | Description |
|------|-------------|
| `wrds_analysis.ipynb` | Complete Python analysis notebook |
| `README.md` | This file |

## How to Reproduce

1. Ensure you have an active WRDS account with PostgreSQL access
2. Clone this repository
3. Create virtual environment: `python -m venv venv`
4. Activate environment and install dependencies: `pip install wrds pandas matplotlib seaborn keyring`
5. The notebook will prompt for your WRDS credentials upon first run
6. Run `wrds_analysis.ipynb` in order (Jupyter Notebook / VS Code)

**Note**: The data download may take 1-2 minutes due to the large volume (approx. 2.4 million rows for 2024).

## Dependencies
- Python 3.9+
- wrds
- pandas
- matplotlib
- seaborn
- keyring

## Limitations

1. **Single-year analysis** (2024 only) – Does not capture multi-year patterns or regime changes
2. **US-focused data** – CRSP covers only US-listed securities; findings may not generalize to international markets
3. **No control variables** – Analysis does not control for industry, liquidity, or other confounding factors
4. **Survivorship bias** – CRSP includes only actively traded securities during the period
5. **Simple volatility measure** – Uses only historical standard deviation; does not incorporate implied volatility or downside risk metrics

## Next Steps / Extensions

- Extend analysis to multiple years to test stability of findings
- Control for industry and liquidity effects
- Compare with implied volatility (VIX) for large-cap vs. small-cap
- Incorporate downside volatility (semi-deviation) to capture asymmetric risk
- Test volatility clustering using GARCH models

## AI Use Disclosure

| Tool | Model/Version | Access Date | Purpose |
|------|---------------|-------------|---------|
| ChatGPT | GPT-4 (OpenAI) | April 2026 | Code structure assistance, markdown formatting, README drafting |

The Python analysis, data interpretation, and all substantive insights are my own work. AI tools were used only for organizational and formatting support.

## References

- CRSP (Center for Research in Security Prices). (2024). CRSP Daily Stock File. WRDS.
- Fama, E. F., & French, K. R. (1993). Common risk factors in the returns on stocks and bonds. *Journal of Financial Economics*, 33(1), 3-56.

## Author
Zixuan Huang
- Student ID: 2469525
- Module: ACC102
- Track: Track 2 – GitHub Data Analysis Project
- Submission Date: April 23, 2026

## Demo Video
https://b23.tv/SMueqoB