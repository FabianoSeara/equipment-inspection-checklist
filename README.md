# 🛠️ Equipment Inspection Checklist

Command-line interface (CLI) system to manage safety inspections for port equipment (RTG and Reach Stacker): inspector login, item-by-item checklist, inspection history, and equipment release/block.

This project was born from my practical experience as a crane operator at a port terminal, where safety inspections are part of the daily routine. The goal was to recreate this process as a real application, with a database and user authentication.

## Features

- **Login with authentication:** each inspector has a name and registration number; the password (registration number) is stored as a hash, never in plain text. 3 attempts before access block.
- **Structured checklist:** iterates through 8 verification items (tires, cables, horn, cameras, emergency buttons, glass, oil, water), recording status (OK/Issue) and observations when there is a problem.
- **Equipment validation:** only accepts pre-registered equipment numbers (RTG-01 to RTG-08, RS-01 to RS-04), preventing typos.
- **Final result controlled by the inspector:** Released or Blocked — the decision is always manual, never automatic, reflecting the real safety process.
- **Inspection history:** query with optional filter by equipment.

## Technologies

- Python 3 (no external dependencies)
- SQLite (local database via the standard library `sqlite3` module)
- `hashlib` (password hashing, standard library)

## Project Structure

```text
equipment-inspection-checklist/
├── main.py          # Terminal menu, login, and interaction screens
├── operacoes.py     # Business logic (login, register inspection, list...)
├── database.py      # SQLite connection and table creation
└── README.md



## Data Model

Three related tables:

- inspectors — name and registration number (hash) of those who can log into the system.

- inspections — general data of each inspection (machine, inspector, date, result).

- inspection_items — each checklist item, linked to the corresponding inspection by foreign key (inspection_id).



## How to Run

No dependencies to install — just Python 3.

git clone https://github.com/FabianoSeara/equipment-inspection-checklist.git
cd equipment-inspection-checklist
python main.py


The database (inspecoes.db) is created automatically on the first run.


**Test Inspectors registered:**
| Name | Registration(Password)
|------|-----------|
| Ricardo | 20 |
| Rafael | 21 |
| Fabiano | 22 |
| João | 23 |



## Next Steps

- [ ] Also validate the machine type (RTG/RS) against a fixed list
- [ ] Display checklist items on the listing screen, not just the summary
- [ ] Screen to register new inspectors directly from the menu
- [ ] Export inspection reports to PDF or CSV

---

Project developed by [Fabiano Seára](https://github.com/FabianoSeara) as part of my portfolio for transitioning to a software development career, with AI (Claude) assistance in the learning process.
