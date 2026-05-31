-- =====================================================================
-- VIEW DATA
-- =====================================================================

SELECT *
FROM workspace.default.car_sales_data
LIMIT 100;

-- =====================================================================
-- CREATE TABLE
-- =====================================================================

CREATE OR REPLACE TABLE car_sales (
    year INT,
    make STRING,
    model STRING,
    body STRING,
    state STRING,
    sellingprice FLOAT,
    mmr FLOAT,
    odometer BIGINT,
    saledate STRING
);

-- =====================================================================
-- CALCULATE TOTAL REVENUE
-- =====================================================================

UPDATE workspace.default.car_sales_data
SET total_revenue = sellingprice;

-- =====================================================================
-- CALCULATE PROFIT MARGIN
-- =====================================================================

UPDATE workspace.default.car_sales_data
SET profit_margin =
((sellingprice - mmr) / sellingprice) * 100;

-- =====================================================================
-- CREATE PERFORMANCE TIERS
-- =====================================================================

UPDATE workspace.default.car_sales_data
SET performance_tier =
CASE
    WHEN profit_margin >= 25 THEN 'High Margin'
    WHEN profit_margin >= 15 THEN 'Medium Margin'
    ELSE 'Low Margin'
END;

-- =====================================================================
-- TOTAL REVENUE
-- =====================================================================

SELECT
    SUM(total_revenue) AS total_revenue
FROM workspace.default.car_sales_data;

-- =====================================================================
-- TOTAL UNITS SOLD
-- =====================================================================

SELECT
    COUNT(*) AS total_cars_sold
FROM workspace.default.car_sales_data;

-- =====================================================================
-- AVERAGE SELLING PRICE
-- =====================================================================

SELECT
    AVG(sellingprice) AS avg_selling_price
FROM workspace.default.car_sales_data;

-- =====================================================================
-- AVERAGE PROFIT MARGIN
-- =====================================================================

SELECT
    AVG(profit_margin) AS avg_profit_margin
FROM workspace.default.car_sales_data;

-- =====================================================================
-- REVENUE BY CAR MAKE
-- =====================================================================

SELECT
    make,
    SUM(total_revenue) AS revenue
FROM workspace.default.car_sales_data
GROUP BY make
ORDER BY revenue DESC;

-- =====================================================================
-- BEST SELLING MODELS
-- =====================================================================

SELECT
    model,
    COUNT(*) AS total_cars_sold
FROM workspace.default.car_sales_data
GROUP BY model
ORDER BY total_cars_sold DESC;

-- =====================================================================
-- REVENUE BY REGION
-- =====================================================================

SELECT
    state,
    SUM(total_revenue) AS revenue
FROM workspace.default.car_sales_data
GROUP BY state
ORDER BY revenue DESC;

-- =====================================================================
-- SALES BY BODY TYPE
-- =====================================================================

SELECT
    body,
    COUNT(*) AS total_sales
FROM workspace.default.car_sales_data
GROUP BY body
ORDER BY total_sales DESC;

-- =====================================================================
-- AVERAGE SELLING PRICE BY YEAR
-- =====================================================================

SELECT
    year,
    AVG(sellingprice) AS avg_selling_price
FROM workspace.default.car_sales_data
GROUP BY year
ORDER BY year;

-- =====================================================================
-- MONTHLY SALES TREND
-- =====================================================================

SET legacy_time_parser_policy = LEGACY;

SELECT
    MONTH(to_timestamp(saledate)) AS sales_month,
    SUM(sellingprice) AS monthly_revenue
FROM workspace.default.car_sales_data
GROUP BY MONTH(to_timestamp(saledate))
ORDER BY sales_month;

-- =====================================================================
-- QUARTERLY SALES TREND
-- =====================================================================

SELECT
    QUARTER(to_timestamp(saledate)) AS sales_quarter,
    SUM(total_revenue) AS quarterly_revenue
FROM workspace.default.car_sales_data
GROUP BY QUARTER(to_timestamp(saledate))
ORDER BY sales_quarter DESC;

-- =====================================================================
-- YEARLY SALES TREND
-- =====================================================================

SELECT
    YEAR(to_timestamp(saledate)) AS sales_year,
    SUM(sellingprice) AS yearly_revenue
FROM workspace.default.car_sales_data
GROUP BY YEAR(to_timestamp(saledate))
ORDER BY sales_year;

-- =====================================================================
-- HIGH MARGIN VEHICLES
-- =====================================================================

SELECT
    make,
    model,
    profit_margin
FROM workspace.default.car_sales_data
WHERE performance_tier = 'High Margin'
ORDER BY profit_margin DESC;

-- =====================================================================
-- LOW MARGIN VEHICLES
-- =====================================================================

SELECT
    make,
    model,
    profit_margin
FROM workspace.default.car_sales_data
WHERE performance_tier = 'Low Margin'
ORDER BY profit_margin ASC;

-- =====================================================================
-- TOP 5 REVENUE GENERATING VEHICLES
-- =====================================================================

SELECT
    make,
    model,
    SUM(total_revenue) AS revenue
FROM workspace.default.car_sales_data
GROUP BY make, model
ORDER BY revenue DESC
LIMIT 5;

-- =====================================================================
-- MILEAGE VS SELLING PRICE
-- =====================================================================

SELECT
    odometer,
    sellingprice
FROM workspace.default.car_sales_data
ORDER BY odometer;

-- =====================================================================
-- MOST POPULAR MANUFACTURING YEAR
-- =====================================================================

SELECT
    year,
    COUNT(*) AS vehicles_sold
FROM workspace.default.car_sales_data
GROUP BY year
ORDER BY vehicles_sold DESC;

-- =====================================================================
-- REVENUE BY PERFORMANCE TIER
-- =====================================================================

SELECT
    performance_tier,
    SUM(total_revenue) AS revenue
FROM workspace.default.car_sales_data
GROUP BY performance_tier
ORDER BY revenue DESC;

-- =====================================================================
-- TOP REGION BY SALES VOLUME
-- =====================================================================

SELECT
    state,
    COUNT(*) AS total_cars_sold
FROM workspace.default.car_sales_data
GROUP BY state
ORDER BY total_cars_sold DESC;

-- =====================================================================
-- TOP BODY TYPE BY REVENUE
-- =====================================================================

SELECT
    body,
    SUM(total_revenue) AS revenue
FROM workspace.default.car_sales_data
GROUP BY body
ORDER BY revenue DESC;

-- =====================================================================
-- DUPLICATE CHECK
-- =====================================================================

SELECT
    vin,
    COUNT(*) AS duplicate_count
FROM workspace.default.car_sales_data
GROUP BY vin
HAVING COUNT(*) > 1;

-- =====================================================================
-- NULL VALUE CHECK
-- =====================================================================

SELECT *
FROM workspace.default.car_sales_data
WHERE make IS NULL
   OR model IS NULL
   OR sellingprice IS NULL
   OR mmr IS NULL
   OR state IS NULL;

-- =====================================================================
-- TOP 10 MOST EXPENSIVE VEHICLES
-- =====================================================================

SELECT
    make,
    model,
    sellingprice
FROM workspace.default.car_sales_data
ORDER BY sellingprice DESC
LIMIT 10;

-- =====================================================================
-- CHEAPEST VEHICLES
-- =====================================================================

SELECT
    make,
    model,
    sellingprice
FROM workspace.default.car_sales_data
ORDER BY sellingprice ASC
LIMIT 10;
