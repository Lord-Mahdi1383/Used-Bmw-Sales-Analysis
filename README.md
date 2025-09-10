# Overview    
This repository extracts BMW data from a larger dataset, cleans it, and performs an analysis to find hidden relationships. These insights are essential for someone running a website for selling used cars, particularly BMWs, aiding in pricing, inventory selection, and sales strategy     

## Extracting BMW data      
- used a try-except block for error handling
- Processed the large dataset in chunks of 10,000 rows for memory efficiency        
- while extracting we can use:    
  - ```header=None```: the oroginal dataset lacks headers  
  - ```on_bad_lines='skip``` to skip malformed rows instead of crashing    
  - ```quoting=3```, ```quotechar=None```, ```escapechar='\\'```: Handles non-standard quoting and escaping.   
- after extracting BMW vehicles from each chunk:    
  - lower case the 'make' column        
  - add them to our bmw_chunk empty list (declared after chunk_size)    
  - after extracting all BMW datas we combine all those chunks into a single dataframe and save it as a CSV file

## Cleaning The Extracted BMW Data
- drop rows we don't need: 'make', 'vin'  
- fill NaN values in transimission column with 'Unknown' then map it to 0-2 and convert to uint8 to make it more memory efficient  
- converting 'state' and 'seller' column to category datatype for later plotting    
- fill NaN values in 'condition' and 'odometer' with their median value  
- fill NaN values in 'body' column with 'Unknown' then lower case it and remove any leading or trailing whitespces, at last label encode it and covert to uint8 to save memory  
- fill NaN values in 'color' and 'interior' column with most common value then label encode these column and convert to uint8  
- make two new column (sale_date_only, sale_time_only) from 'sale_date' and drop it afterwarsds  
- making a new column from 'sale_date_only' by extracting just the year     
- make a new column by subtracting 'year' from 'sale_year'    
- calculating price difference by subtracting 'mmr' from 'selling_price'

# Dataset Analysis And Plotting
making 18 different plots to analyse and catch hidden relationships
we used:
- box plot to catch outliers in selling price
- heatmap for numerical featues
- pairplot
- scatter plot for:
  - car age vs odometer
  - odometer vs selling price
  - car age vs mmr and selling price
  - mmr vs selling price
- histogram plot for:
  - mmr
  - selling price
  - price difference
  - odometer
  - condition
  - car age 
- bar plot for:
  - transmission type
  - average selling price by transmission type
  - interior
  - color
  - top 10 models sorted by their average selling price
  - car sales by hour of day, day of week and month
- pie chart for:
  - body type
  - transmission type
  - AM and PM sales
- horizontal bar for:
  - total bmw sales by model
  - total sales revenue by model
  - average sale by model

# Setup
### Clone The Repository
``` bash
git clone https://github.com/Lord-Mahdi1383/Used-Bmw-Sales-Analysis.git
cd Used-Bmw-Sales-Analysis
```

### Install Requirements
``` bash
pip install -r Requirements.txt
```
