# Commonwealth Bank — Data Science Job Simulation

> End-to-end data work for a major Australian bank: aggregation, privacy-compliant anonymisation, analytics proposal, and relational database design.
> Completed as part of the **Commonwealth Bank Introduction to Data Science Job Simulation** on Forage.

![Excel](https://img.shields.io/badge/Excel-SUMIFS-217346?logo=microsoftexcel&logoColor=white)
![Python](https://img.shields.io/badge/Python-Anonymisation-blue?logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-Schema_Design-336791?logo=postgresql&logoColor=white)
![CommBank](https://img.shields.io/badge/CommBank-Forage_Simulation-FEE105)

---

## 📌 Project Summary

This simulation replicates four real tasks a data analyst might handle at CommBank within a single week:

1. **Quantitative analysis** on transactional data for a partner company (InsightSpark)
2. **Privacy-compliant anonymisation** of a sensitive customer dataset
3. **Business proposal writing** — how to extract commercial value from public social media data
4. **Relational database design** for storing and querying social media signals

Together the four tasks span the full spectrum of junior DA work — **data engineering, analytics, consulting, and architecture** — framed within the Australian financial services context.

---

## 🗂️ Repository Structure

```
commbank-data-science-simulation/
├── README.md
├── task1-data-aggregation/
│   ├── Supermarket_Analysis.xlsx                # SUMIFS analysis with live formulas
│   └── notes.md                                 # Questions, answers, methodology
├── task2-data-anonymisation/
│   ├── anonymisation_pipeline.py                # Python pipeline (suppression, generalisation, derivation)
│   ├── mobile_customers_anonymised.csv          # Final anonymised dataset
│   └── notes.md                                 # Technique rationale and column-by-column decisions
├── task3-analytics-proposal/
│   └── Twitter_Proposal.pdf                     # Business proposal: 6 use cases for @CommBank Twitter data
└── task4-database-design/
    ├── Database_Design.pdf                      # Full schema proposal with rationale
    └── schema.sql                               # CREATE TABLE statements
```

---

## 🎯 Task-by-Task Highlights

### Task 1 — Data Aggregation & Analysis (Excel)

Analysed 50,783 supermarket transactions across 48 stores to answer three stakeholder questions using **SUMIFS** with live, inspectable formulas:

| Question | Answer | Formula |
|---|---|---|
| Apples purchased in cash (quantity) | **117 units** | `=SUMIFS(qty, product, "apple", payment, "cash")` |
| Total cash spent on apples | **$537.03** | `=SUMIFS(total, product, "apple", payment, "cash")` |
| Bakershire non-member total spend | **$2,857.51** | `=SUMIFS(total, store, "Bakershire", customer, "non-member")` |

**Design choice:** the submission file keeps formulas live (not hardcoded values) so any team lead can inspect and reuse the logic — a small detail, but exactly what the brief requested.

### Task 2 — Data Anonymisation (Python)

Reduced a 19-column PII-heavy customer dataset to 9 analytically useful columns using three standard techniques:

- **Suppression** — dropped direct identifiers (name, username, email, full address, credit card number, CVV, birthdate, GPS coordinates, employer)
- **Generalisation** — age → 6 brackets; salary → 7 brackets; address → state only; registration date → year-month
- **Derivation** — added `tenure_months` as a retention-analysis-ready metric

Result: analytical utility preserved for segmentation, demographics, and tenure analysis. Re-identification risk minimised. Compliant with Australian Privacy Act 1988 principles.

### Task 3 — Business Proposal (Written)

Proposed six commercial use cases for publicly available @CommBank Twitter data:

1. Customer sentiment tracking
2. Customer service performance monitoring
3. Topic & theme detection (emerging complaints)
4. Competitive benchmarking vs NAB, Westpac, ANZ
5. Campaign effectiveness analysis
6. Fraud & scam signal detection

Each framed with methodology, refresh cadence, expected business value, and compliance consideration.

### Task 4 — Database Design (Schema)

Designed a 3NF relational database to store @CommBank tweets, replies, quote retweets, and direct mentions. Five tables with clear primary keys, foreign keys, and many-to-many resolution via link tables:

| Table | Purpose | Key Relationship |
|---|---|---|
| `Users` | Every Twitter account observed | — |
| `Tweets` | Every tweet (original, reply, quote, mention) | FK → Users; self-FK for threads |
| `Mentions` | Link table: tweets ↔ mentioned users | M2M resolver |
| `Hashtags` | Distinct hashtags | — |
| `TweetHashtags` | Link table: tweets ↔ hashtags | M2M resolver |

**Key design decision:** a single `Tweets` table with a `tweet_type` column rather than four separate tables. Avoids schema duplication and makes cross-type engagement analysis a single query instead of a four-way UNION.

---

## 🧰 Tech Stack

- **Excel** — SUMIFS, conditional aggregation, formula documentation
- **Python 3.10** — pandas for data manipulation, regex for parsing
- **SQL** — relational schema design (3NF), surrogate keys, link tables
- **Markdown / Word** — business proposal and design document authoring

---

## 📜 Certification

Completed as part of the [Commonwealth Bank Introduction to Data Science Job Simulation](https://www.theforage.com/simulations/commonwealth-bank/intro-data-science-sd7t) hosted on Forage, April 2026.

---

## 👤 Author

**Ahmed Al Rafsan** — Data Analyst | MBIS (Data Analytics), AIH Melbourne

🔗 [LinkedIn](https://www.linkedin.com/in/ahmed-al-rafsan-/) · 💻 [GitHub](https://github.com/Ahmed-Al-Rafsan) · ▶️ [YouTube — Rafsan Data & AI Lab](https://www.youtube.com/@AhmedAlRafsan)


---

*This work is for portfolio and educational purposes only. No proprietary Commonwealth Bank data is redistributed.*
