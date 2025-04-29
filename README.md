<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
</head>
<body>

  <h1>📊 Supply Chain Analytics with SQL</h1>
  <p><strong>Author:</strong> Rahul Mahapatra<br>
     <strong>Domain:</strong> Supply Chain Optimization | Data Analysis | SQL</p>

  <h2>📌 Project Overview</h2>
  <p>Conducted an end-to-end analysis of a supply chain dataset using SQL to derive actionable insights on:</p>
  <ul>
    <li><strong>Revenue optimization</strong> (top-performing products, supplier revenue)</li>
    <li><strong>Operational efficiency</strong> (lead times, shipping costs, routes)</li>
    <li><strong>Risk assessment</strong> (supplier inspection failures, stock shortages)</li>
  </ul>
  <p><strong>Database:</strong> supply_chain | <strong>Tools:</strong> MySQL</p>

  <h2>🗃️ Database Schema</h2>
  <pre><code>
CREATE TABLE supply_chain (
  Product_type VARCHAR(50),
  SKU VARCHAR(50),
  Price DECIMAL(10, 2),
  available_quantity INT,
  sold_quantity INT,
  revenue_generated DECIMAL(15,2),
  Gender ENUM("nonbinary","Male","Female"),
  Stock_level INT,
  fulfillment_lead_time INT,
  Order_quantitie INT,
  Shipping_time INT,
  Shipping_carrier VARCHAR(50),
  Shipping_cost DECIMAL(15, 2),
  Supplier_name VARCHAR(100),
  Location VARCHAR(100),
  Supplier_lead_time INT,
  Production_volume INT,
  Manufacturing_lead_time INT,
  Manufacturing_cost DECIMAL(15, 2),
  Inspection_result VARCHAR(50),
  Transportation_mode VARCHAR(50),
  Routes VARCHAR(50),
  Cost DECIMAL(15, 2)
);
  </code></pre>

  <h2>🔍 SQL Queries & Insights</h2>

  <h3>Q1. Total Revenue by Product Category</h3>
  <pre><code>
SELECT product_type, SUM(revenue_generated) AS total_revenue 
FROM supply_chain 
GROUP BY product_type 
ORDER BY total_revenue DESC;
  </code></pre>
  <p><strong>Insight:</strong> Skincare products drive the highest revenue.</p>

  <h3>Q2. Average Fulfillment Lead Time by Supplier</h3>
  <pre><code>
SELECT supplier_name, AVG(fulfillment_lead_time) AS avg_lead_time 
FROM supply_chain 
GROUP BY supplier_name;
  </code></pre>
  <p><strong>Insight:</strong> Nivea has the fastest fulfillment (14.3 days).</p>

  <h3>Q3. Top 5 Low-Stock Products (Stock &lt; 50)</h3>
  <pre><code>
SELECT SKU, stock_level 
FROM supply_chain 
WHERE stock_level &lt; 50 
ORDER BY stock_level DESC 
LIMIT 5;
  </code></pre>
  <p><strong>Action:</strong> Replenish SKU28 and SKU81 immediately.</p>

  <h3>Q4. Total Manufacturing Cost by Supplier</h3>
  <pre><code>
SELECT supplier_name, SUM(Manufacturing_cost) AS total_cost 
FROM supply_chain 
GROUP BY supplier_name 
ORDER BY total_cost;
  </code></pre>
  <p><strong>Insight:</strong> Nivea is the most cost-efficient supplier.</p>

  <h3>Q5. Top Supplier by Quantity Supplied</h3>
  <pre><code>
SELECT supplier_name, SUM(Order_quantitie) AS total_quantity 
FROM supply_chain 
GROUP BY supplier_name 
ORDER BY total_quantity DESC 
LIMIT 1;
  </code></pre>
  <p><strong>Insight:</strong> Unilever is the largest volume supplier.</p>

  <h3>Q6. Average Shipping Cost by Transportation Mode</h3>
  <pre><code>
SELECT Transportation_mode, ROUND(AVG(Shipping_cost),2) AS avg_cost 
FROM supply_chain 
GROUP BY Transportation_mode 
ORDER BY avg_cost DESC;
  </code></pre>
  <p><strong>Recommendation:</strong> Use Sea transport for cost savings.</p>

  <h3>Q7. Products with Highest Sales Volume</h3>
  <pre><code>
SELECT product_type, SUM(revenue_generated) AS total_revenue 
FROM supply_chain 
GROUP BY product_type 
ORDER BY total_revenue DESC;
  </code></pre>
  <p><strong>Note:</strong> Same as Q1 – skincare is top-performing.</p>

  <h3>Q8. Mumbai Suppliers with Revenue &gt; 30,000</h3>
  <pre><code>
SELECT supplier_name, SUM(revenue_generated) AS total_revenue 
FROM supply_chain 
WHERE location = "Mumbai" 
GROUP BY supplier_name 
HAVING total_revenue &gt; 30000;
  </code></pre>
  <p><strong>Insight:</strong> Unilever dominates Mumbai’s revenue.</p>

  <h3>Q9. Top 5 Products with Long Lead Times (&gt;27 days)</h3>
  <pre><code>
SELECT SKU, Supplier_lead_time 
FROM supply_chain 
WHERE Supplier_lead_time &gt; 27 
ORDER BY Supplier_lead_time DESC 
LIMIT 5;
  </code></pre>
  <p><strong>Risk:</strong> SKU139 has the longest delay (30 days).</p>

  <h3>Q10. Most Used Transportation Modes</h3>
  <pre><code>
SELECT Transportation_mode, SUM(sold_quantity) AS total_shipped 
FROM supply_chain 
GROUP BY Transportation_mode 
ORDER BY total_shipped DESC;
  </code></pre>
  <p><strong>Insight:</strong> Rail is the most popular shipping method.</p>

  <h3>Q11. Supplier Inspection Failures</h3>
  <pre><code>
SELECT supplier_name, COUNT(Inspection_result) AS failed_inspections 
FROM supply_chain 
WHERE Inspection_result = "fail" 
GROUP BY supplier_name;
  </code></pre>
  <p><strong>Critical Issue:</strong> P&G has the highest failure rate.</p>

  <h3>Q12. Suppliers with Highest Lead Time Variance</h3>
  <pre><code>
SELECT supplier_name, 
       MAX(Supplier_lead_time) - MIN(Supplier_lead_time) AS variance 
FROM supply_chain 
GROUP BY supplier_name 
ORDER BY variance DESC;
  </code></pre>
  <p><strong>Risk:</strong> Loreal’s inconsistent lead times may disrupt planning.</p>

  <h3>Q13. Most Cost-Effective Routes</h3>
  <pre><code>
SELECT Routes, AVG(Cost) AS avg_cost 
FROM supply_chain 
GROUP BY Routes 
ORDER BY avg_cost;
  </code></pre>
  <p><strong>Recommendation:</strong> Prioritize Route A for cost efficiency.</p>

  <h2>📊 Key Takeaways</h2>
  <ul>
    <li><strong>Revenue:</strong> Skincare is the top revenue generator ($241K).</li>
    <li><strong>Efficiency:</strong> Nivea has the fastest fulfillment (14.3 days).</li>
    <li><strong>Cost:</strong> Route A is the cheapest ($485/unit).</li>
    <li><strong>Risk:</strong> P&G has 12 inspection failures – needs audit.</li>
  </ul>

</body>
</html>
