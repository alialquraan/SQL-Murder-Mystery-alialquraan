# explain_indexed.md — After Indexing

> Re-run the same 8 queries after applying your indexes from `indexes.sql`.
> Compare with `explain_baseline.md` — look for SCAN → SEARCH improvements.

---

## Q1 — All murders in SQL City

**Execution Time:** ___ ms *(baseline: ___ ms | change: ___)*
**Scan Type:** Index Search
**Index Used:** idx_crime_city_type

```
-- Paste EXPLAIN QUERY PLAN output here
```
SEARCH TABLE crime_scene_report USING INDEX idx_crime_city_type (city=? AND type=?)

USE TEMP B-TREE FOR ORDER BY
---

## Q2 — People with their driver's license details

**Execution Time:** ___ ms *(baseline: ___ ms | change: ___)*
**Scan Type:** SCAN TABLE person / SEARCH TABLE drivers_license
**Index Used:** INTEGER PRIMARY KE

```
-- Paste EXPLAIN QUERY PLAN output here
```
SCAN TABLE person AS p

SEARCH TABLE drivers_license AS dl USING INTEGER PRIMARY KEY (rowid=?)

USE TEMP B-TREE FOR ORDER BY
---

## Q3 — Gym members who checked in on January 9, 2018

**Execution Time:** ___ ms *(baseline: ___ ms | change: ___)*
**Scan Type:** Index Search
**Index Used:** idx_checkin_date

```
-- Paste EXPLAIN QUERY PLAN output here
```
SEARCH TABLE get_fit_now_check_in AS ci USING INDEX idx_checkin_date (check_in_date=?)

SEARCH TABLE get_fit_now_member AS m USING INDEX sqlite_autoindex_get_fit_now_member_1 (id=?)

USE TEMP B-TREE FOR ORDER BY
---

## Q4 — Gold gym members and their income

**Execution Time:** ___ ms *(baseline: ___ ms | change: ___)*
**Scan Type:** SCAN TABLE member / SEARCH TABLE person & income
**Index Used:** INTEGER PRIMARY KEY

```
-- Paste EXPLAIN QUERY PLAN output here
```
SCAN TABLE get_fit_now_member AS m

SEARCH TABLE person AS p USING INTEGER PRIMARY KEY (rowid=?)

SEARCH TABLE income AS i USING INTEGER PRIMARY KEY (rowid=?)

USE TEMP B-TREE FOR ORDER BY

---

## Q5 — People who attended Facebook events in 2018

**Execution Time:** ___ ms *(baseline: ___ ms | change: ___)*
**Scan Type:** Index Search
**Index Used:** idx_facebook_date

```
-- Paste EXPLAIN QUERY PLAN output here
```
SEARCH TABLE facebook_event_checkin AS fe USING INDEX idx_facebook_date (date>? AND date<?)

SEARCH TABLE person AS p USING INTEGER PRIMARY KEY (rowid=?)
---

## Q6 — Red-haired Tesla drivers

**Execution Time:** ___ ms *(baseline: ___ ms | change: ___)*
**Scan Type:** SCAN TABLE person / SEARCH TABLE drivers_license
**Index Used:** INTEGER PRIMARY KEY

```
-- Paste EXPLAIN QUERY PLAN output here
```
SCAN TABLE person AS p

SEARCH TABLE drivers_license AS dl USING INTEGER PRIMARY KEY (rowid=?)

USE TEMP B-TREE FOR ORDER BY
---

## Q7 — Interview transcripts mentioning the gym or murder

**Execution Time:** ___ ms *(baseline: ___ ms | change: ___)*
**Scan Type:** SCAN TABLE interview / SEARCH TABLE person
**Index Used:** None / INTEGER PRIMARY KEY

```
-- Paste EXPLAIN QUERY PLAN output here
```
SCAN TABLE interview AS i

SEARCH TABLE person AS p USING INTEGER PRIMARY KEY (rowid=?)

---

## Q8 — Average income by car make

**Execution Time:** ___ ms *(baseline: ___ ms | change: ___)*
**Scan Type:** SCAN TABLE person / SEARCH TABLE drivers_license & income
**Index Used:** INTEGER PRIMARY KEY

```
-- Paste EXPLAIN QUERY PLAN output here
```
SCAN TABLE person AS p

SEARCH TABLE drivers_license AS dl USING INTEGER PRIMARY KEY (rowid=?)

SEARCH TABLE income AS i USING INTEGER PRIMARY KEY (rowid=?)

USE TEMP B-TREE FOR GROUP BY

USE TEMP B-TREE FOR ORDER BY