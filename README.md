
>> # BELEZATORY

Hey there!

This mini project involves working with data from an Excel file to create a crowdfunding database. Here are the steps you'll need to follow:

Create a Category DataFrame and a Subcategory DataFrame by extracting data from the Excel file and saving them as CSV files.

Create a Campaign DataFrame by extracting data from the Excel file and saving it as a CSV file.

Create a Contacts DataFrame by either using Python dictionary methods or regular expressions to extract data from the Excel file and save it as a CSV file.

Use the data from the CSV files to create a database schema for a Postgres database.

Import the CSV files into the Postgres database and verify that the data is correct.


You can view the Code in the file: ETL_Mini_Project_Starter_Code.ipynb
The supporting docs with SQL work can be found in resources.

Thanks !

BELEZA!

=======
## Create a Contacts DataFrame that has the following columns:**
- A column named "contact_id"  that contains the unique number of the contact person.
- A column named "first_name" that contains the first name of the contact person.
- A column named "last_name" that contains the first name of the contact person.
- A column named "email" that contains the email address of the contact person

Then export the DataFrame as a `contacts.csv` CSV file.

## Campaign DataFrame
----
**Create a Campaign DataFrame that has the following columns:**
- The "cf_id" column.
- The "contact_id" column.
- The “company_name” column.
- The "blurb" column is renamed as "description."
- The "goal" column.
- The "goal" column is converted to a `float` datatype.
- The "pledged" column is converted to a `float` datatype. 
- The "backers_count" column. 
- The "country" column.
- The "currency" column.
- The "launched_at" column is renamed as "launch_date" and converted to a datetime format. 
- The "deadline" column is renamed as "end_date" and converted to a datetime format.
- The "category_id" with the unique number matching the “category_id” from the category DataFrame. 
- The "subcategory_id" with the unique number matching the “subcategory_id” from the subcategory DataFrame.
- And, create a column that contains the unique four-digit contact ID number from the `contact.xlsx` file.
Then export the DataFrame as a `campaign.csv` CSV file.

>> # Crowdfunding Data Processing

This project involves processing and organizing crowdfunding data using Python and pandas. The provided code performs various operations on the data, such as merging, cleaning, and exporting the data into separate CSV files. Here's a step-by-step guide on how to use the code:

## Getting Started

1. Make sure you have Python installed on your system.
2. Install the necessary dependencies by running the following command:
   ```
   pip install pandas numpy
   ```
3. Download the crowdfunding data file ("crowdfunding.xlsx") and place it in the "Resources" directory.

## Code Overview

The code provided performs the following tasks:

1. Importing Dependencies: The necessary libraries, including pandas, numpy, json, and re, are imported.
2. Reading the Crowdfunding Data: The crowdfunding data is read from the "crowdfunding.xlsx" file and stored in a pandas DataFrame called `crowdfunding_info_df`.
3. Summary of the Crowdfunding Data: A brief summary of the `crowdfunding_info_df` DataFrame is displayed.
4. Extracting Category and Subcategory Values: The `category & sub-category` column is split into two separate columns, 'category' and 'subcategory', using the '/' delimiter. These new columns are added to the `crowdfunding_info_df` DataFrame.
5. Getting Unique Categories and Subcategories: Lists of unique categories and subcategories are created using the `category` and `subcategory` columns from the DataFrame.
6. Creating Category and Subcategory DataFrames: Separate DataFrames (`category_df` and `subcategory_df`) are created for categories and subcategories, respectively, with their corresponding IDs and names.
7. Exporting Category and Subcategory Data: The `category_df` and `subcategory_df` DataFrames are exported as CSV files named "category.csv" and "subcategory.csv", respectively, in the "Resources" directory.
8. Data Cleaning and Transformation: A copy of the `crowdfunding_info_df` DataFrame named `campaign_df` is created. Column names 'blurb', 'launched_at', and 'deadline' are renamed to 'description', 'launched_date', and 'end_date', respectively. The 'goal' and 'pledged' columns are converted to float data type. The 'launched_date' and 'end_date' columns are formatted as datetime.
9. Merging DataFrames: The `campaign_df` DataFrame is merged with the `category_df` and `subcategory_df` DataFrames based on the "category" and "subcategory" columns, respectively. The merged DataFrame is stored in `merged_df`.
10. Dropping Unwanted Columns: Unnecessary columns ('staff_pick', 'spotlight', 'category & sub-category', and 'category') are dropped from the `merged_df` DataFrame.
11. Exporting the Cleaned Data: The cleaned `merged_df` DataFrame is exported as a CSV file named "campaign.csv" in the "Resources" directory.
12. Processing Contacts Data: The contacts data is read from the "contacts.xlsx" file, skipping the first two rows, and stored in a pandas DataFrame called `contact_info_df`.
13. Creating Contacts DataFrame: A new DataFrame, `contacts_df`, is created with columns 'contact_id', 'first_name', 'last_name', and 'email' from the `contact_info_df`.
14. Exporting Contacts Data: The `contacts_df` DataFrame is exported as a CSV file named "contacts.csv" in the "Resources" directory.

## Usage

1. Ensure that you have placed the input data files (`crowdfunding.xlsx` and `contacts.xlsx`) in the "Resources" directory.
2. Run the Python code in your preferred development environment or command prompt.

## Outputs

The code generates the following output files:

1. `contacts.csv: This file contains the processed contacts data with columns 'contact_id', 'first_name', 'last_name', and 'email'.

campaign.csv: This file contains the processed crowdfunding campaign data with columns 'cf_id', 'contact_id', 'company_name', 'description', 'goal', 'pledged', 'backers_count', 'country', 'currency', 'launch_date', 'end_date', 'category_id', 'subcategory_id', and 'contact_id_4digits'.

category.csv: This file contains the category data with columns 'category_id' and 'category_name'.

subcategory.csv: This file contains the subcategory data with columns 'subcategory_id' and 'subcategory_name'.

## Further Customization

If you want to modify the code for your specific needs, consider the following:

- File Paths: If your input data files or desired output file paths are different, make sure to update the file paths accordingly.
- Data Cleaning: If you need to perform additional data cleaning or transformation steps, you can modify the code within the section "Data Cleaning and Transformation."
- Column Renaming: If you prefer different column names in the final output, you can modify the code where column renaming is performed.
- Dropping Unwanted Columns: If you want to keep or drop different columns from the merged DataFrame, you can modify the code within the section "Dropping Unwanted Columns."

Feel free to adapt the code to suit your specific requirements.

### Conclusion

This README provides an overview of the provided code for processing crowdfunding data. By following the instructions and executing the code, you can generate cleaned and organized CSV files containing contacts and campaign information. If you have any questions or encounter any issues, please feel free to reach out for assistance.

 ---
 ```python
 # Import dependencies
import pandas as pd
import numpy as np
import json
import re
pd.set_option('max_colwidth', 400)
```

```python
# Read the data into a Pandas DataFrame
crowdfunding_info_df = pd.read_excel('Resources/crowdfunding.xlsx')
crowdfunding_info_df.head()

# Get a brief summary of the crowdfunding_info DataFrame.

crowdfunding_info_df.head()

# Get the crowdfunding_info_df columns.
columns = crowdfunding_info_df.columns
columns
```

### Assign the category and subcategory values to category and subcategory columns.

```python
crowdfunding_info_df[['category', 'subcategory']] = crowdfunding_info_df['category & sub-category'].str.split('/', expand=True)


crowdfunding_info_df.head()
```

```python
# Get the unique categories and subcategories in separate lists.
categories= crowdfunding_info_df.category.unique()
subcategories= crowdfunding_info_df.subcategory.unique()
print(f'The unique categories are: {categories}')
print(              )
print(f'The unique subcategories are: {subcategories}')
# Get the number of distinct values in the categories and subcategories lists.
print(len(categories))
print(len(subcategories))
```
```python
# Create numpy arrays from 1-9 for the categories and 1-24 for the subcategories.
category_ids = np.arange(1, 10)
subcategory_ids = np.arange(1, 25)

# Use a list comprehension to add "cat" to each category_id. 
cat_ids=[f"cat{category_id}" for category_id in category_ids]

# Use a list comprehension to add "subcat" to each subcategory_id.    
# scat_ids=[f"cat{subcategory_ids}" for subcategory_id in subcategory_ids]

scat_ids = ["scat0" + str(scat_id) for scat_id in subcategory_ids]
```


### Create a category DataFrame with the category_id array as the category_id and categories list as the category name.
```python
category_dict = {'category_id': cat_ids, 'category_name': categories}
category_df = pd.DataFrame(category_dict)
```

### Create a category DataFrame with the subcategory_id array as the subcategory_id and subcategories list as the subcategory name. 
subcategory_dict = {'subcategory_id': scat_ids, 'subcategory_name': subcategories}


subcategory_df = pd.DataFrame(subcategory_dict)

```python
# subcategory_df
# Export categories_df and subcategories_df as CSV files.
category_df.to_csv("Resources/category.csv", index=False)

subcategory_df.to_csv("Resources/subcategory.csv", index=False)
# Create a copy of the crowdfunding_info_df DataFrame name campaign_df. 
campaign_df = crowdfunding_info_df.copy()
campaign_df.head()
# Rename the blurb, launched_at, and deadline columns.

campaign_df = campaign_df.rename(columns={'blurb': 'description', 'launched_at': 'launched_date', 'deadline': 'end_date'})


campaign_df
```

```python
# Convert the goal and pledged columns to a `float` data type.
campaign_df['goal'] = campaign_df['goal'].astype(float)
campaign_df['pledged'] = campaign_df['pledged'].astype(float)
campaign_df.dtypes

# Format the launched_date and end_date columns to datetime format
from datetime import datetime as dt
campaign_df['launched_date'] = pd.to_datetime(campaign_df['launched_date'], unit="s").dt.date
campaign_df['end_date'] = pd.to_datetime(campaign_df['end_date'], unit="s").dt.date
```

###Merge the campaign_df with the category_df on the "category" column and the subcategory_df on the "subcategory" column.

```python
merged_df=pd.merge(campaign_df, category_df, on='category')
```

```python
# campaign_merged_df = pd.merge(campaign_merged_df, subcategory_df, on='subcategory')

merged_df = pd.merge(merged_df, subcategory_df, on='subcategory')

merged_df.head()
```

```python
# Drop unwanted columns

merged_df.drop(columns=['staff_pick', 'spotlight', 'category & sub-category', 'category'], inplace=True)

merged_df
```

### Export the DataFrame as a CSV file. 
```python
campaign_cleaned = merged_df
campaign_cleaned.to_csv("Resources/campaign.csv", index=False)
```

### Read the data into a Pandas DataFrame. Use the `header=2` parameter when reading in the data.
```python
contact_info_df = pd.read_excel('Resources/contacts.xlsx', header=2)
contact_info_df.head()
```

>>>>>>> Stashed changes
