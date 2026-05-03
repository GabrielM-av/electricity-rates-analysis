
# electricity-rates-analysis

Analysis of U.S. Electric Utility Rates by Zip Code (2024)

This project analyzes electricity rates across U.S. zip codes using the
U.S. Electric Utility Companies and Rates dataset from Data.gov.

The goal is to identify which zip codes have the highest residential
electricity rates and determine whether Investor Owned utilities
tend to have higher rates than other ownership types.

Dataset:
U.S. Electric Utility Companies and Rates: Look-up by Zip Code (2024)
Source: Data.gov / National Renewable Energy Laboratory (NREL)

## Commands Used

### Extract relevant columns
awk -F',' '{print $1","$4","$3","$6","$9}' electricity_rates_2024.csv > selected_rates.csv

### Sort by highest residential rate
sort -t',' -k5 -nr selected_rates.csv > sorted_rates.txt

### Get top 10 highest rates
head -10 sorted_rates.txt > top10_res_rates.txt

### Compare average residential rates by state and ownership
awk -F',' 'NR>1 {sum[$2","$4]+=$5; count[$2","$4]++} END {for (key in sum) print key","sum[key]/count[key]}' selected_rates.csv > avg_res_rate_by_state_ownership.csv
