# India General Elections 2024 – Result Analysis

A collection of SQL queries and explanations for analysing the official **India General Elections 2024** results. The project explores questions such as total seats by state, alliance‑wise performance, constituency‑level winners, and more.

---

## 📂 Project Structure

```
.
├── DDL/                 # (optional) schema creation scripts
├── data/                # raw CSVs / JSON exports of the six tables
├── queries/             # individual `.sql` files for each problem statement
└── README.md            # <– you are here
```

> **Note**: Only the `README.md` is provided here. Feel free to reorganise directories or add notebooks / BI dashboards as you expand the repo.

---

## 🗃️ Database Schema

The analysis expects six tables in a SQL Server database named `ELECTION_DB`.

| Table | Purpose |
|-------|---------|
| **`states`** | Master list of Indian States & UTs (one row per state) |
| **`statewise_results`** | 2024 results aggregated at state level (state‑wise vote counts & seat wins) |
| **`constituencywise_results`** | One row per Lok Sabha constituency with winner, margin, etc. |
| **`constituencywise_details`** | Vote break‑up for **every** candidate in a constituency |
| **`partywise_results`** | National view: total seats/votes won by each party |
| **`partywise_results`** | 👉 _will be altered in this repo_ to add a `party_alliance` column |

> If you do **not** already have these tables, load them from `data/*.csv` and run the DDL in `DDL/`.

---

## 🚀 Quick Start

```sql
-- 1️⃣ Switch to the election DB
USE ELECTION_DB;

-- 2️⃣ Peek at the raw data
SELECT TOP 5 * FROM constituencywise_results;
```

---

## 📈 Problem Statements & Queries

Below is a compact index. Each query lives in `queries/` as a dedicated `.sql` file so you can copy‑paste or run via your favourite SQL client.

| # | Description | File |
|---|-------------|------|
| 01 | **Total Lok Sabha seats** across the country | `01_total_seats.sql` |
| 02 | Seats available **by state** | `02_seats_by_state.sql` |
| 03 | Seats won by the **NDA alliance** | `03_nda_total.sql` |
| 04 | Breakdown of **NDA seats** per party | `04_nda_partywise.sql` |
| 05 | Seats won by the **I.N.D.I.A alliance** | `05_india_total.sql` |
| 06 | Breakdown of **I.N.D.I.A seats** per party | `06_india_partywise.sql` |
| 07 | Add & populate a `party_alliance` column | `07_add_alliance_column.sql` |
| 08 | **Which alliance won the most seats?** | `08_alliance_comparison.sql` |
| 09 | Winner, party & margin for any seat | `09_constituency_winner.sql` |
| 10a | Vote distribution for **all** candidates in a seat | `10a_vote_distribution.sql` |
| 10b | Party performance in a **given state** | `10b_state_party_seats.sql` |
| 11 | Alliance‑wise seat tally **per state** | `11_state_alliance_matrix.sql` |
| 12 | **Top‑10 vote getters** (EVM votes) | `12_top10_evms.sql` |
| 13 | Winner vs Runner‑up for every seat in a state | `13_winner_runnerup.sql` |
| 14 | Maharashtra summary – seats, votes, parties, etc. | `14_maharashtra_summary.sql` |

### Example – Problem Statement 03

`queries/03_nda_total.sql`:

```sql
-- Total seats won by NDA alliance
SELECT SUM(CASE
           WHEN Party IN (
               'Apna Dal (Soneylal) - ADAL', 'Asom Gana Parishad - AGP',
               'Bharatiya Janata Party - BJP', 'Hindustani Awam Morcha (Secular) - HAMS',
               'Janasena Party - JnP', 'Janata Dal (Secular) - JD(S)',
               'Janata Dal (United) - JD(U)', 'Lok Janshakti Party(Ram Vilas) - LJPRV',
               'Nationalist Congress Party - NCP', 'Rashtriya Janata Dal - RJD',
               'Rashtriya Lok Dal - RLD', 'Shiv Sena - SHS',
               'Sikkim Krantikari Morcha - SKM', 'Telugu Desam - TDP')
           THEN [won] ELSE 0 END) AS NDA_Total_Seats_Won
FROM partywise_results;
```

Run it in SQL Server Management Studio (SSMS) or Azure Data Studio and you should see **the NDA’s national seat count**.

---

## ⚙️ Conventions

* **Snake case** for column aliases (`total_seats`) and directory names.
* SQL keywords in **UPPERCASE**, identifiers in `PascalCase` as per original Election Commission naming.
* Queries kept idempotent & safe: destructive commands (`ALTER`, `UPDATE`) flagged clearly.

---

## 📝 License

Feel free to fork or adapt. Attribution is appreciated but not required.

---

## 🙌 Acknowledgements

* Election data courtesy of the **Election Commission of India** (public domain).
* SQL Server used for illustration – adapt the syntax (`TOP 10`, square‑bracket quoting) if you are on Postgres/MySQL.

---

### ✨ Happy querying! ✨