# Core KPI Measures

This file contains the base KPIs used across the Search Analytics dashboard.
These measures form the foundation for all higher-level analysis.

---

## Total Searches

**Definition:**  
Total number of search events.

**DAX:**
```DAX
Total Searches =
COUNTROWS ( fact_search )

Zero Result Searches

Definition:
Searches that returned zero products, indicating catalog gaps.

DAX:

Zero Result Searches =
CALCULATE (
    [Total Searches],
    fact_search[is_zero_result] = TRUE()
)

Low Result Searches

Definition:
Searches that returned fewer than 3 products, indicating weak catalog coverage.

DAX:

Low Result Searches =
CALCULATE (
    [Total Searches],
    fact_search[is_low_result] = TRUE()
)

Search Fail Rate

Definition:
Percentage of searches that failed to meet user intent.

Fail = Zero Result + Low Result

DAX:

Search Fail Rate (%) =
DIVIDE (
    [Zero Result Searches] + [Low Result Searches],
    [Total Searches],
    0
)

Key Notes

All KPIs are filter-aware

Measures respect date, category, brand, and keyword slicers

Boolean flags are handled at the data model level


---

## 📄 `dax/trends.md`

```markdown
# Trend Measures (Time-Based Analysis)

This file contains measures used to analyze trends and growth over time,
including week-over-week (WoW) comparisons.

---

## Previous Week Searches

**Definition:**  
Total searches from the previous week, aligned by week start date.

**DAX:**
```DAX
Previous Week Searches =
VAR ThisWeek =
    MAX ( dim_date[week_start_date] )
VAR PrevWeek =
    ThisWeek - 7
RETURN
CALCULATE (
    [Total Searches],
    FILTER (
        ALL ( dim_date ),
        dim_date[week_start_date] = PrevWeek
    )
)

Week-over-Week Growth %

Definition:
Percentage change in searches compared to the previous week.

DAX:

WoW Growth % =
VAR Prev = [Previous Week Searches]
VAR Curr = [Total Searches]
RETURN
IF (
    Prev = 0,
    BLANK(),
    DIVIDE ( Curr - Prev, Prev )
)

Keyword-Level WoW Growth

Definition:
Week-over-week growth calculated at the keyword level to identify trending or viral search terms.

DAX:

Keyword WoW Growth % =
VAR Prev = [Previous Week Searches]
VAR Curr = [Total Searches]
RETURN
IF (
    Prev = 0,
    BLANK(),
    DIVIDE ( Curr - Prev, Prev )
)

Key Notes

Week-based analysis uses week_start_date

BLANK() is used instead of 0% to avoid misleading growth values

Measures automatically adapt to keyword context via relationships


---

## 📄 `dax/intent_measures.md`

```markdown
# User Intent Measures

This file contains measures used to understand user intent related to
price sensitivity, rating preferences, and product attributes.

---

## Searches with Price Filter

**Definition:**  
Number of searches where users applied a price filter.

**DAX:**
```DAX
Searches with Price Filter =
CALCULATE (
    [Total Searches],
    fact_search[has_price_filter] = TRUE()
)

% Searches with Price Filter

Definition:
Percentage of users showing price sensitivity.

DAX:

% Searches with Price Filter =
DIVIDE (
    [Searches with Price Filter],
    [Total Searches],
    0
)

Average Minimum Price

Definition:
Average minimum price specified in search filters.

DAX:

Avg Min Price =
AVERAGE ( fact_search[Min Price] )

Average Maximum Price

Definition:
Average maximum price specified in search filters.

DAX:

Avg Max Price =
AVERAGE ( fact_search[Max Price] )

Searches with Rating Filter

Definition:
Number of searches where users applied a rating filter.

DAX:

Searches with Rating Filter =
CALCULATE (
    [Total Searches],
    fact_search[has_rating_filter] = TRUE()
)

% Searches with Rating Filter

Definition:
Percentage of users who consider ratings during search.

DAX:

% Searches with Rating Filter =
DIVIDE (
    [Searches with Rating Filter],
    [Total Searches],
    0
)

Attribute-Based Searches (Example: Pigmentation)

Definition:
Searches associated with specific product attributes using structured attribute mapping.

DAX:

Pigmentation Searches =
CALCULATE (
    [Total Searches],
    fact_search[is_pigmentation_search] = TRUE()
)

Key Notes

Attribute measures are based on structured Attributes field

Intent measures are fully filter-aware

These KPIs support merchandising and UX decisions
