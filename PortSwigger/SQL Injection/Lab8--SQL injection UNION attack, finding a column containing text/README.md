# Lab-8: SQL injection UNION attack, finding a column containing text

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you first need to determine the number of columns returned by the query.The next step is to identify a column that is compatible with string data. 

**Aim :-** The lab will provide a random value that you need to make appear within the query results. To solve the lab, perform a SQL injection UNION attack that returns an additional row containing the value provided. This technique helps you determine which columns are compatible with string data. 


## Solution
- To determine the number of columns use the following payload
    ``` ' UNION SELECT null,null,null -- ```
    - Only 3 null returns a valid response otherwise it gives an internal server error
    - So there is only **3 columns**

- Check which column returns a string 
    - To check whether the columns contains text or not put random strings instead of null and make the request
    - Only ``` ' UNION SELECT null,'abc',null -- ``` returns a valid response otherwise its a internal server error

- Return the row with the value provided
    ``` ' UNION SELECT null,'<value-to-return>',null -- ```