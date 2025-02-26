-- Step 1: Create the Wholesale Revenue Table (if not exists)
CREATE TABLE WholesaleRevenue (
    OrderID INT PRIMARY KEY,
    OrderDate DATE,
    ProductLine VARCHAR(255),
    Warehouse VARCHAR(255),
    NetRevenue DECIMAL(10,2)
);

-- Step 2: Insert Sample Data
INSERT INTO WholesaleRevenue (OrderID, OrderDate, ProductLine, Warehouse, NetRevenue) VALUES
(1, '2024-06-15', 'Electronics', 'Warehouse A', 5000.00),
(2, '2024-06-20', 'Clothing', 'Warehouse B', 3200.00),
(3, '2024-07-05', 'Electronics', 'Warehouse A', 6700.00),
(4, '2024-07-15', 'Furniture', 'Warehouse C', 4200.00),
(5, '2024-08-10', 'Clothing', 'Warehouse B', 2900.00),
(6, '2024-08-18', 'Electronics', 'Warehouse C', 5100.00);

-- Step 3: Analyze Revenue Trends by Month
SELECT 
    TO_CHAR(OrderDate, 'YYYY-MM') AS Month,
    ProductLine,
    SUM(NetRevenue) AS TotalRevenue
FROM WholesaleRevenue
WHERE OrderDate BETWEEN '2024-06-01' AND '2024-08-31'
GROUP BY Month, ProductLine
ORDER BY Month, TotalRevenue DESC;

-- Step 4: Analyze Revenue Trends by Warehouse
SELECT 
    Warehouse,
    SUM(NetRevenue) AS TotalRevenue
FROM WholesaleRevenue
WHERE OrderDate BETWEEN '2024-06-01' AND '2024-08-31'
GROUP BY Warehouse
ORDER BY TotalRevenue DESC;

-- Step 5: Identify Top-Selling Product Lines
SELECT 
    ProductLine,
    SUM(NetRevenue) AS TotalRevenue
FROM WholesaleRevenue
WHERE OrderDate BETWEEN '2024-06-01' AND '2024-08-31'
GROUP BY ProductLine
ORDER BY TotalRevenue DESC
LIMIT 5;



