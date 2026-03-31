# explain_baseline.md — Before Indexing

> Run each query with `EXPLAIN QUERY PLAN` and paste the output below.
> Also run `.timer on` before each query to capture execution time.
>
> **Connect:** `sqlite3 sql-murder-mystery.db`
> Then type: `.timer on`

---

## Q1 — All murders in SQL City

**Execution Time:** ___ ms
**Scan Type:** SCAN TABLE
**Notes:** 

```
-- Paste EXPLAIN QUERY PLAN output here
```
SCAN TABLE crime_scene_report
---

## Q2 — People with their driver's license details

**Execution Time:** ___ ms
**Scan Type:** SCAN TABLE person
**Notes:** 

```
-- Paste EXPLAIN QUERY PLAN output here
```
SCAN TABLE person AS p

SEARCH TABLE drivers_license AS dl USING INTEGER PRIMARY KEY (rowid=?)

USE TEMP B-TREE FOR ORDER BY
---

## Q3 — Gym members who checked in on January 9, 2018

**Execution Time:** ___ ms
**Scan Type:** SCAN TABLE get_fit_now_check_in
**Notes:** ___

```
-- Paste EXPLAIN QUERY PLAN output here
```
SCAN TABLE get_fit_now_check_in AS ci

SEARCH TABLE get_fit_now_member AS m USING INDEX sqlite_autoindex_get_fit_now_member_1 (id=?)

USE TEMP B-TREE FOR ORDER BY

---

## Q4 — Gold gym members and their income

**Execution Time:** ___ ms
**Scan Type:** SCAN TABLE get_fit_now_member
**Notes:** ___

```
-- Paste EXPLAIN QUERY PLAN output here
```
SCAN TABLE get_fit_now_member AS m

SEARCH TABLE person AS p USING INTEGER PRIMARY KEY (rowid=?)

SEARCH TABLE income AS i USING INTEGER PRIMARY KEY (rowid=?)

USE TEMP B-TREE FOR ORDER BY
---

## Q5 — People who attended Facebook events in 2018

**Execution Time:** ___ ms
**Scan Type:** SCAN TABLE facebook_event_checkin
**Notes:** ___

```
-- Paste EXPLAIN QUERY PLAN output here
```
SCAN TABLE facebook_event_checkin AS fe

SEARCH TABLE person AS p USING INTEGER PRIMARY KEY (rowid=?)

USE TEMP B-TREE FOR ORDER BY
---

## Q6 — Red-haired Tesla drivers

**Execution Time:** ___ ms
**Scan Type:** SCAN TABLE person
**Notes:** ___

```
-- Paste EXPLAIN QUERY PLAN output here
```
SCAN TABLE person AS p

SEARCH TABLE drivers_license AS dl USING INTEGER PRIMARY KEY (rowid=?)

USE TEMP B-TREE FOR ORDER BY
---

## Q7 — Interview transcripts mentioning the gym or murder

**Execution Time:** ___ ms
**Scan Type:** SCAN TABLE interview
**Notes:** ___

```
-- Paste EXPLAIN QUERY PLAN output here
```
SCAN TABLE interview AS i

SEARCH TABLE person AS p USING INTEGER PRIMARY KEY (rowid=?)
---

## Q8 — Average income by car make

**Execution Time:** ___ ms
**Scan Type:** SCAN TABLE person
**Notes:** ___

```
-- Paste EXPLAIN QUERY PLAN output here
```
SCAN TABLE person AS p

SEARCH TABLE drivers_license AS dl USING INTEGER PRIMARY KEY (rowid=?)

SEARCH TABLE income AS i USING INTEGER PRIMARY KEY (rowid=?)

USE TEMP B-TREE FOR GROUP BY

USE TEMP B-TREE FOR ORDER BY