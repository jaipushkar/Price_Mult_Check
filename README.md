# Price_Mult_Check

ThriveMarket Price Mult Check
This repository contains a SQL query for identifying and analyzing product descriptions in the ThriveMarket dataset to check for inconsistencies related to pack sizes and price multipliers.

Overview
The provided SQL query retrieves product descriptions and corresponding price multipliers from the ThriveMarket dataset. It filters the results to identify descriptions containing pack-related keywords (e.g., 'Pack', 'N-Pack') and where the price multiplier (price_mult) is either NULL or does not appear in the description. Additionally, it ensures that the eindicator column does not contain the letter 'w'.

SQL Query
_**SELECT
    description,
    price_mult
FROM
    Backup_ThriveMarket_09_20_2023
WHERE
    (
        description LIKE '%[0-9] Pack%'
        OR description LIKE '%[0-9]-Pack%'
        OR description LIKE '%Pack%'
    )
    AND (
        price_mult IS NULL 
        OR description NOT LIKE '%' + price_mult + '%' 
    )
    AND (
        CHARINDEX(' Pack', description) > 0 -- Description contains ' Pack'
        OR CHARINDEX('-Pack', description) > 0 -- Description contains '-Pack'
    )
    AND (
        PATINDEX('%[0-9] Pack%', description) > 0 
        OR PATINDEX('%[0-9]-Pack%', description) > 0
        OR PATINDEX('%[0-9] Pack', description) > 0 
        OR PATINDEX('%[0-9]-Pack', description) > 0 
    )
    AND eindicator NOT LIKE '%w%';**_
    
Description
This SQL query is designed to identify products in the ThriveMarket dataset where the description suggests a pack size (e.g., '6 Pack', 'N-Pack') but either the price_mult column is NULL or the price multiplier does not appear in the description. It aims to highlight potential inconsistencies or missing information in the dataset.

How to Use
Clone this repository to your local machine.
Execute the provided SQL query in your SQL Server environment, replacing Backup_ThriveMarket_09_20_2023 with the appropriate table name if necessary.
Review the output to identify products that meet the specified criteria.
Use the insights gained from the query results to address any inconsistencies or missing information in the dataset.
