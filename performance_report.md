# Performance Report — SQL Murder Mystery Index Investigation

**Student Name:** Ali Alquraan
**Date:** 3/31/2026
**Database:** `sql-murder-mystery.db` (SQLite)

---

## Summary Table

| Query | Baseline (ms) | Indexed (ms) | Improvement | Index Used? |
|-------|--------------|-------------|-------------|-------------|
| Q1 — Murders in SQL City | High |Low|Significant| |
| Q2 — People + license details |High| Medium|Moderate| |
| Q3 — Gym check-ins Jan 9 | High |Low|Significant| |
| Q4 — Gold members + income |High| Medium|Moderate| |
| Q5 — Facebook events 2018 | High |Low|Significant| |
| Q6 — Red-haired Tesla drivers |High| Medium|Moderate| |
| Q7 — Interview keyword search |High | High|None| |
| Q8 — Income by car make |High| Medium|Moderate| |

---

## 1. Queries That Improved the Most

*Which queries got faster? By how much? Why did the index help for those specific queries?*

Q1, Q3, and Q5 showed the most significant improvement Because we created specific B-Tree indexes on the columns used
---

## 2. Queries That Did NOT Improve

*Which queries showed little or no change? Explain why — think about table size, the use of `LIKE '%...'` wildcards, or cases where a full scan is actually faster.*

Q7 (Interview keyword search) showed no improvement.The query uses LIKE '%gym%'. Since the wildcard % is at the beginning of the search string, the database cannot use a standard index to find the match and is forced to perform a full table scan to check every character in the transcripts.
---

## 3. Tradeoffs of Indexing

*Discuss:*
- How indexes speed up SELECT/WHERE/JOIN operations
Pros: Indexes drastically speed up SELECT queries, especially those involving JOIN operations and complex WHERE filters.

- How indexes slow down INSERT, UPDATE, DELETE
Cons: Every index we add slows down INSERT, UPDATE, and DELETE operations because the database must update the index file every time data changes.

- Storage overhead (each index takes extra disk space)
Storage: Indexes occupy extra disk space. In a massive database, indexing every column would lead to "Storage Bloat."

- Why you wouldn't index every column
Decision: We only index columns that are frequently used for searching or joining to maintain a balance between speed and storage.
---

## 4. Production Recommendation

*If this were a real police database handling thousands of queries per day, which indexes would you keep? Which would you drop? Justify your choices with evidence from your measurements.*

Keep: I would definitely keep idx_crime_city_type and the indexes on license_id and person_id. These are high-traffic columns in a police database.

Drop: I would reconsider adding a dedicated index for membership_status if the "Gold" members represent a large percentage of the table, as a full scan might sometimes be more efficient for very common values.

Justification: Our tests showed that joining tables using indexed foreign keys is much more stable and scalable than relying on full scans, which would crash a real-world system with millions of records.
---

*© 2026 LevelUp Economy. All rights reserved.*
