
# Purchases Application processes
> This application is responsible for:
> 1. Ingest the raw data from transactions.csv file
> 2. Execute the full data pipeline: ingesting the transactions file data using Python + dbt process.

![alt text](https://geomarketing.com/wp-content/uploads/2015/12/purchase-path.png)

## Data Files used as source:

__transactions__ - contains transaction history for all customers for a period of at least 1 year prior to their offered incentive
- __id__ - A unique id representing a customer
- __chain__ - An integer representing a store chain
- __dept__ - An aggregate grouping of the Category (e.g. water)
- __category__ - The product category (e.g. sparkling water)
- __company__ - An id of the company that sells the item
- __brand__ - An id of the brand to which the item belongs
- __date__ - The date of purchase
- __productsize__ - The amount of the product purchase (e.g. 16 oz of water)
- __productmeasure__ - The units of the product purchase (e.g. ounces)
- __purchasequantity__ - The number of units purchased
- __purchaseamount__ - The dollar amount of the purchase

__offers__ - contains information about the offers
- __offer__ - An id representing a certain offer
- __category__ - The product category (e.g. sparkling water)
- __quantity__ - The number of units one must purchase to get the discount
- __company__ - An id of the company that sells the item
- __offervalue__ - The dollar value of the offer
- __brand__ -  An id of the brand to which the item belongs

The transactions file can be joined to the offers file by (category, brand, company). A negative value in productquantity and purchaseamount indicates a return.

Reference:  
https://www.kaggle.com/c/acquire-valued-shoppers-challenge/data?select=offers.csv.gz  


## Technical Description:

The project is responsible to run the full data pipeline (the Python application + dbt):
| Technology | Project | Description |
| ------ | ------ | ------ |
| ![alt text](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSyHZ2NYrS9J4TdreA31eou6fAWfNgQ1hUemZY_Klj2mNiaV2t43w&s) | [data-ingestion-purchases](https://github.com/jmilhomem/data-ingestion-purchases) | Project that ingests a large transaction csv file and executes the full data pipeline: ingests data + does the transformation for it|
| ![alt text](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSYWYTxOJiMjop_GT6sDsXtMUpVyyw8HKyiENnbv2JsTJX_Fs8_lw&s) | [dbt_purchases_project](https://github.com/jmilhomem/dbt_purchases_project) | Project that execute the full data pipeline using dbt |

## Dependencies:
To execute the full data pipeline (__data-ingestion-purchases/main_etl_processes.py__ application):
* get dbt installed and the [dbt dbt_purchases_project cloned](https://github.com/jmilhomem/dbt_purchases_project) 
* get dbt installed and the [python data-ingestion-purchases cloned](https://github.com/jmilhomem/data-ingestion-purchases) 
* a Postgres database instance created at AWS RDS.
* config.ini file filled and available in __~/.config__ folder (Check the data-ingestion-purchases detailed information)
* profiles.yml file filled and available in __~/.dbt__ folder (Check the dbt_purchases_project detailed information)
* python 3.6
* make  
