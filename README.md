# mutual-funds-ml-pipeline

1. Raw data storage
The original MutualFunds.csv dataset is stored in Google Cloud Storage in my bucket called conor-weekes-data-20084449. The file is stored inside the raw/ folder and I will keep this version unchanged. I will keep the original version so that if I make a mistake during preprocessing, or decide to change how the data is cleaned later, I can recreate the processed dataset from the original file.

2. Processed data storage and file formats
The processed version of the dataset is sotored separate "Sharded/" folder in the same Google Cloud Storage bucket. The original dataset is stored as a CSV file. After preprocessing, I plan to store the processed dataset in Parquet format.
I chose Parquet because the dataset contains a large number of columns and is mainly made up of structured numerical and categorical data.
