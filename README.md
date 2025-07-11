#Retrieve the order id and the number of months between order date and payment date for all orders.
SELECT 
    orderid,
    MONTHS_BETWEEN(Orderdate, Pymtdate) AS "No of Months"
FROM orders;

#Display current date as 'Mon/DD/YYYY Day'
SELECT TO_CHAR(SYSDATE, 'Mon/DD/YYYY Day') AS CURRENTDATE
FROM DUAL;

#Display numeric part of retail outlet id
SELECT 
    TO_NUMBER(REGEXP_SUBSTR(Roid, '\d+')) AS NUMERICROID
FROM 
    Retailoutlet;

#Retrieve the employee id, employee name of billing staff and the retail outlet where they work. Perform a case insensitive search.
SELECT 
  Empid AS EMPID, 
  Empname AS EMPNAME, 
  Worksin AS WORKSIN
FROM Empdetails
WHERE 
  LOWER(Designation) = 'billing staff';


#For a discount of 25.5% being offered on all FMCG item's unit price, display item code, existing unit price as "Old Price" and discounted price as "New Price ". Round off the discounted price to two decimal values.
SELECT 
  Itemcode,
  Price AS "Old Price",
  ROUND(Price * (1 - 0.255), 2) AS "New Price"
FROM 
  Item
WHERE 
  LOWER(Itemtype) = 'fmcg';

#The management of EasyShop would like to classify the salary of employees as Class 3, Class 2 and Class 1. The classification is done as if salary is less than 2500 then the class is 'Class 3' , if between 2500 and 5000 then 'Class 2', and if salary is more than 5000 then 'Class 1'. Write a query to display EmpId, Salary and classification of salary.
SELECT 
  Empid, 
  Salary,
  CASE 
    WHEN Salary < 2500 THEN 'Class 3'
    WHEN Salary BETWEEN 2500 AND 5000 THEN 'Class 2'
    WHEN Salary > 5000 THEN 'Class 1'
  END AS SALGRADE
FROM 
  Empdetails;



#Salary hikes are being given to all employees of EasyShop based on their role. The percentage increase is as given below. Write a query to display EmpId, EmpName, Salary and increased salary.

Designation(Role)	Hike in %
Administrator	10
Manager	5
Billing Staff	20
Security	25
Others	2

SELECT 
  Empid, 
  Empname, 
  Salary, 
  ROUND(
    CASE 
      WHEN Designation = 'Administrator' THEN Salary * 1.10
      WHEN Designation = 'Manager' THEN Salary * 1.05
      WHEN Designation = 'Billing Staff' THEN Salary * 1.20
      WHEN Designation = 'Security' THEN Salary * 1.25
      ELSE Salary * 1.02
    END, 2
  ) AS "INCREASEDSALARY"
FROM 
  Empdetails;


#Display the full Month name from string representation of date stored in "Jan/10/2015" format. Also display the amount 2,50,000 by converting it as 250000 as "Amount". Use dual table to perform above operation.
SELECT 
  TO_CHAR(TO_DATE('Jan/10/2015', 'Mon/DD/YYYY'), 'Month') AS "MONTH",
  TO_NUMBER(REPLACE('2,50,000', ',', '')) AS "AMOUNT"
FROM 
  DUAL;



#Write a query to display the sale id, no. of months between the saledate and today's date as "MONTH_AGED" for all the sales. Show positive values for no. of months and round it to 1 decimal places.
SELECT 
  Saleid,
  ROUND(ABS(MONTHS_BETWEEN(SYSDATE, Sldate)), 1) AS "MONTH_AGED"
FROM 
  Sale;


#Exercise 31 : Functions

A discount of 22.5% being offered on all sports category item's unit price, Write a query to display product id, product description, existing unit price as "Old_Price" and discounted price as "New_Price" for sports category item. Round off the discounted price to two decimal places.
SELECT 
  Prodid,
  Pdesc,
  Price AS "Old_Price",
  ROUND(Price * (1 - 0.225), 2) AS "New_Price"
FROM 
  Product
WHERE 
  LOWER(Category) = 'sports';



  #
Collaborative Assignment 43

The salary of managers has been increased by 20%. Retrieve the empid, existing salary as "Current Salary", increased salary as "New Salary" and the difference of existing and increased salary as "Incremented Amount". Round off the increased salary up to two decimal places.
SELECT 
  Empid,
  Salary AS "Current Salary",
  ROUND(Salary * 1.20, 2) AS "New Salary",
  ROUND((Salary * 1.20) - Salary, 2) AS "Incremented Amount"
FROM 
  Empdetails
WHERE 
  Designation = 'Manager';

