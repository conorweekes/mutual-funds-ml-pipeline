# mutual-funds-ml-pipeline

1. Raw data storage
The original MutualFunds.csv dataset is stored in Google Cloud Storage in my bucket called conor-weekes-data-20084449. The file is stored inside the raw/ folder and I will keep this version unchanged. I will keep the original version so that if I make a mistake during preprocessing, or decide to change how the data is cleaned later, I can recreate the processed dataset from the original file.

The link can be found here: https://storage.googleapis.com/conor-weekes-data-20084449/raw/MutualFunds.csv

3. Processed data storage and file formats
The processed version of the dataset is stored separate "Sharded/" folder in the same Google Cloud Storage bucket. The original dataset is stored as a CSV file. After preprocessing, I plan to store the processed dataset in Parquet format.

The link can be found here: https://console.cloud.google.com/storage/browser/conor-weekes-data-20084449

![Database object storage decision](./3%20Database%20object%20storage%20decision.png)

4. Database / object storage decision
For this project I will use Google Cloud Storage instead of a database. The project mainly uses one CSV dataset which is stored in GSCV bucket (https://storage.googleapis.com/conor-weekes-data-20084449/raw/MutualFunds.csv).

5. Data versioning
I used Google Cloud Storage versioning rather than keeping separate copies of the dataset manually. This means older versions of a file can still be recovered if the data is changed or overwritten. I would keep the most recent 3 versions of each file and keep older versions for around 30 days before removing them. This should be enough for the project without keeping unnecessary copies for too long.

6. Data access
I split the dataset into 80% training data, 10% development data and 10% test data. I then compared the distribution of fund_category across the three datasets to check that the different fund categories remained represented at similar proportions. To reduce the risk of data leakage, I kept the test data separate from the training process.

