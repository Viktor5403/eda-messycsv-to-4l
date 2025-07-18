# 🚀 Data Triage: “Messy CSV → ₹ 4 L Savings”  

**A compact end‑to‑end EDA project** demonstrating how a 72 MB, header‑less, multi‑format CSV dump can be triaged in **7 quick steps** to uncover **₹ 4 ,01 ,728** in prevented losses—all packaged as a 6‑page PDF carousel for LinkedIn.  

---

## 📚 Project Context  

Ever received a giant sales export that looks more like a hot mess than a data source? That was our starting point:

1. **14 date formats**, phantom columns, mixed currencies, nulls everywhere.  
2. Manual cleanup promised a half‑day slog—and still might miss the real culprit.  
3. We needed a **rapid**, **reproducible** workflow to:  
   - ➡️ Spot the **return‑spike months**  
   - ➡️ Quantify **orders & revenue lost**  
   - ➡️ Push a **pre‑flight alert** into the BI dashboard  

The result? In **7 lines of code** we went from chaos to clarity, finding **three “villain” months** (May, Aug, Dec) tied to an over‑generous “HolidayBOGO” coupon—and showing how a simple `assert` could flash a red warning next time returns exceed 15 %.

---

## 📂 Repository Contents  

- `annex1.csv` – Item master (codes, names, categories)  
- `annex2.csv` – Transaction log (Date, Time, Item Code, Qty, Price, Sale/Return, Discount)  
- `annex3.csv` – Wholesale costs by date & item  
- `annex4.csv` – Per‑item loss rate (%)  
- `Data Triage - Chaos.ipynb` – Cleaned Jupyter notebook (9 cells)  
- `Data_Triage_Chaos_to_4L_Savings.pdf` – 6‑page LinkedIn carousel ready for upload  

---

## 🔍 What We Did: 7‑Step EDA Workflow  

1. **Load & parse** all four sheets, drop 212 duplicate rows  
2. **Inspect** schema (`df.info()`) & missing values (`.isna().sum()`)  
3. **Flag** returns (`Sale or Return == 'Return'`) and compute `ReturnRate`  
4. **Compute** `Sales_INR = Qty × Price_RMB × rate` and  
   `Cost_INR = Qty × Wholesale_RMB × (1 + LossRate) × rate`  
5. **Calculate** `Margin_INR = Sales_INR − Cost_INR`  
6. **Group by month** → bar chart of return volumes → identify top 3 spikes  
7. **Assert** `df['ReturnRate'].max() < 0.15` to pre‑flight future spikes  

---

## 📈 Key Insights & Visuals  

- **Monthly Return Spikes**: May/Aug/Dec drove 1 ,842 lost orders → ₹ 4 ,01 ,728 impact  
- **Sales vs Returns**: Returns remain tiny vs total sales, but concentrated in coupon months  
- **Margin Analysis**: Discounted orders show lower median margin and more deep losses  
- **Category Drill‑Down**: Top 5 categories by return rate spotlight “HolidayBOGO” offenders  
- **Top 10 Loss‑Makers**: SKU‑level table guides targeted pricing or QC interventions  

---

## 🛠️ How to Reproduce Locally  

1. **Clone or download** this repo.  
2. Create & activate a virtual environment:  
   ```bash
   python -m venv .venv
   source .venv/bin/activate   # macOS/Linux  
   .venv\Scripts\activate      # Windows PowerShell (bypass if needed)  

