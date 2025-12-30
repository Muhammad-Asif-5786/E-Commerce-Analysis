# E Commerce Store Analysis


# 📌#  Project Overview

This project analyzes on-site search behavior for an e-commerce platform to uncover user intent, demand patterns, and catalog gaps. The goal is to help business teams improve product assortment, search relevance, navigation, and strategic decision-making using data-driven insights.

The dashboard is built end-to-end using Power BI, covering data cleaning, modeling, DAX measures, visualization, and documentation—following industry best practices.

# 🎯 Business Objectives

The analysis aims to answer key business questions such as:

What are users searching for the most?

Which search terms are trending week-over-week?

Where is the catalog failing to meet demand?

Which brands and categories drive the highest search interest?

How sensitive are users to price and ratings?

What product attributes (e.g., pigmentation, acne, dry skin) are most in demand?

# 🗂️ Dataset Description

Each row in the dataset represents a single search event performed by a user.
The data includes:

Search date & time

Search keywords

Brand and category context

Structured attributes (e.g., skin concerns)

Search result counts

Price and rating filters

#### Dataset link

https://www.kaggle.com/datasets/mohammedasif5786/e-commerce-dataset

# 🧱 Data Modeling

A star schema was implemented for scalability and performance:

Fact Table

fact_search – search-level events and metrics

Dimension Tables

dim_date – calendar attributes (week, month, year)

dim_keyword – cleaned search keywords

dim_brand – brand names

dim_category – product categories

Technical columns and helper fields are hidden to provide a business-friendly semantic layer.

# 📊 Key KPIs & Metrics

The dashboard includes the following KPIs:

Total Searches

Trending Keywords (Week-over-Week Growth)

Zero-Result Searches

Low-Result Searches (< 3 results)

Search Fail Rate

Top Brands & Categories by Search Demand

Attribute Trends (e.g., pigmentation, acne, dry skin)

Price Intent Metrics (avg min/max price, % price-filtered searches)

Rating Sensitivity (% searches using rating filters)

# 📈 Dashboard Structure

The dashboard is designed for executive storytelling:

Top Section: High-level KPIs

Middle Section: Weekly trends and search performance

Bottom Section: Deep dives into keywords, brands, categories, attributes, and intent

Global slicers allow filtering by:

Date (weekly)

Category

Brand

# ⚠️ Data Limitations

Click or bounce data is not available, so high-exit searches cannot be calculated.

Transaction/cart data is not present, so search-to-cart conversion is excluded.

Regional analysis is limited due to lack of geographic fields.

These limitations are clearly documented to maintain analytical transparency.

# 🛠️ Tools & Technologies

Power BI Desktop

Power Query (data cleaning & transformation)

DAX (measures and calculations)

# ✅ Outcome

This project delivers a production-ready analytics dashboard that enables stakeholders to:

Identify demand gaps and emerging trends

Optimize search and navigation

Support merchandising and brand partnership decisions


## 📥 How to Run This Project

1. Clone repository:
git clone https://github.com/Muhamm
2. Open `dashboard/Search_Analytics_Dashboard.pbix` in Power BI Desktop.

3. Review the `data/` folder for dataset schema and notes.

4. See `dax/` folder for measure definitions.

5. `screenshots/` contains slide previews of key visuals.

6. `documentation/Search_Analytics_Documentation.pdf` contains business context, KPIs, and definitions.
ad-Asif-5786/E-Commerce-Analysis.git


