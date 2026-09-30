# mutual-funds-ml-pipeline

1. Raw data storage

The original MutualFunds.csv dataset is stored in Google Cloud Storage in my bucket called conor-weekes-data-20084449. The file is stored inside the raw/ folder and I will keep this version unchanged. I will keep the original version so that if I make a mistake during preprocessing, or decide to change how the data is cleaned later, I can recreate the processed dataset from the original file.

The link can be found here: https://storage.googleapis.com/conor-weekes-data-20084449/raw/MutualFunds.csv

2. Processed data storage and file formats

The processed version of the dataset is stored separate "sharded/" folder in the same Google Cloud Storage bucket. The original dataset is stored as a CSV file. After preprocessing, I plan to store the processed dataset in Parquet format.

The link can be found here: https://console.cloud.google.com/storage/browser/conor-weekes-data-20084449

![Database object storage decision](./3%20Database%20object%20storage%20decision.png)

3. Database / object storage decision

For this project I will use Google Cloud Storage instead of a database. The project mainly uses one CSV dataset which is stored in GSC bucket (https://storage.googleapis.com/conor-weekes-data-20084449/raw/MutualFunds.csv).

5. Data versioning
For this project, Google Cloud Storage versioning allows older versions to be recovered if files are overwritten.

6. Data access

I accessed Google Cloud Storage from Google Colab using Google authentication. This allowed the notebook to access the bucket without storing passwords or service account keys directly in the notebook. 

8. Data split / validation strategy

I split the dataset into 80% training data, 10% development data and 10% test data. I then compared the distribution of fund_category across the three datasets to check that the different fund categories remained represented at similar proportions. To reduce the risk of data leakage, I kept the test data separate from the training process. I also created 8 cross validation folds from the training data only, using fund_category for stratification and random_state=42.

![Data split](./6%20Data%20split.png)

7. Feature description

The target variable selected for the project was fund_return_2021_q1. This is a continuous numerical value representing the return of a mutual fund during the first quarter of 2021. Because the target is numerical, I treated the machine learning task as a regression problem.

The input features selected included fund_return_2020_q4, total_net_assets, fund_yield, fund_category, fund_family, management_name and expense ratio fields. fund_return_2020_q4 was included as a measure of recent fund performance before the target quarter. total_net_assets, fund_yield and the expense ratio fields were numerical features, while fund_category, fund_family and management_name were categorical features.

![Feature description](./7%20Feature%20description.png)

8. Data types and formats

The MutualFunds.csv dataset contains structured tabular data. Numerical features include fund_return_2021_q1, fund_return_2020_q4, total_net_assets, fund_yield and expense ratio fields. Categorical features include fund_category, fund_family and management_name.  

The original dataset was stored in CSV format. The training, development and test datasets were also stored as CSV files in Google Cloud Storage.

9. Reproducibility of data collection

The dataset used for this project was obtained from the Kaggle Mutual Funds dataset. I downloaded the original MutualFunds.csv file and stored an unchanged copy in the raw/ folder of my Google Cloud Storage bucket. Keeping the original CSV unchanged means that the same source data can be used again if the processed datasets need to be recreated.

The raw dataset can be accessed here:
https://storage.googleapis.com/conor-weekes-data-20084449/raw/MutualFunds.csv

Kaggle Link:
https://www.kaggle.com/datasets/stefanoleone992/mutual-funds-and-etfs?resource=download&select=MutualFunds.csv

10. Reproducibility of preprocessing

The preprocessing steps can be reproduced the Jupyter notebook [(View Notebook Here)](https://github.com/conorweekes/mutual-funds-ml-pipeline/blob/main/MutualFunds_Data_Pipeline.ipynb).
The notebook removes rows with missing fund_category values and removes fund categories containing fewer than 10 funds. The remaining data is split into 80% training, 10% development and 10% test data using random_state=42. The split is stratified by fund_category.
Eight cross validation folds are then created from the training data. The train, development, test and cross validation files are saved as CSV files and uploaded to the sharded/ folder in Google Cloud Storage.
