# pandas_100_questions
Pandas examples , We use 3 files: sales_data_set (weekly store-dept sales with IsHoliday), stores_data_set (store id, type, size), and Features_data_set (store-week context: weather, fuel price, markdowns, CPI, unemployment, holidays).
1. sales_data_set.csv – Weekly Sales Data

What this file contains

This dataset records weekly sales at the department level for each store.

Each row = one (Store, Dept, Week) combination.

Columns

Store

Integer ID of the store (e.g., 1, 2, 3, …).

Links to the Store column in both stores_data_set.csv and Features_data_set.csv.

Dept

Integer ID of the department within a store (e.g., 1, 2, 3, …).

Same department numbers can exist in multiple stores.

Date

Week-ending date for that record (e.g., 05/02/2010).

Represents the sales for that particular week.

Needs to be parsed as datetime.

Weekly_Sales

Floating-point number.

Total sales amount for that store–department in that week.

Positive values → sales, negative values → returns/adjustments.

IsHoliday

Boolean (True / False).

Indicates whether that week includes a major holiday (e.g., Thanksgiving, Christmas, etc.).

Useful for analyzing holiday impact on sales.

Granularity

Store-level + Department-level + Weekly
– You can slice by store, by department, by time, or any combination.

2. stores_data_set.csv – Store Information

What this file contains

This dataset describes the static characteristics of each store.

Each row = one store.

Columns

Store

Integer ID of the store (primary key).

Connects to Store in the other two datasets.

Type

Categorical label (e.g., 'A', 'B', 'C').

Represents store format (e.g., supercenter, small format, etc.).

Good for segmenting performance by store type.

Size

Integer representing the store size in square feet (approx).

Larger values indicate larger physical stores.

Useful for metrics like sales per square foot or size-based comparisons.

Granularity

Store-level, static (no dates here)
– One row per store; attributes do not change across time in this dataset.

3. Features_data_set.csv – Store-Week External Features

What this file contains

This dataset contains weekly external/context variables for each store, such as weather, fuel price, promotions (markdowns), and macroeconomic indicators.

Each row = one (Store, Week) record, with extra info about that week.

Columns

Store

Integer store ID.

Links to Store in the other files.

Date

Week-ending date (same idea as in sales_data_set.csv).

Should match the Date in sales when merging.

Temperature

Numeric (float).

Average temperature (in °F) for that store’s region during the week.

Can be used to see how weather affects sales.

Fuel_Price

Numeric (float).

Price of fuel (e.g., gasoline) in the store’s area during that week.

Useful for studying relation between fuel cost and customer spending.

MarkDown1 … MarkDown5

Numeric columns (often with many NaNs).

Represent different types of promotional markdowns (discount budgets) applied in that store-week.

Higher values generally mean more aggressive promotions.

NaN often = no markdown / no promo recorded.

CPI

Consumer Price Index (float).

Measures price level / inflation in that region over time.

Useful for macro-level analysis or controlling for inflation.

Unemployment

Unemployment rate (float) in the store’s region.

Helps analyze the impact of local economic conditions on sales.

IsHoliday

Boolean (True / False).

Same meaning as in sales_data_set.csv: whether this week contains a major holiday.

Important when merging: you usually merge on ['Store', 'Date', 'IsHoliday'].

Granularity

Store-level + Weekly
– One row per store-week; provides context/features for modeling or analysis.

How They Connect (High-Level)

Primary keys & joins

sales_data_set → detailed sales by store–dept–week.

stores_data_set → store-level attributes (type, size).

Features_data_set → store–week context features (weather, fuel, markdowns, CPI, unemployment).
