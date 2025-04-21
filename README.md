# Elevate-labs-Task1 #
1. Folder Structure for GitHub Repo

netflix-data-cleaning/
│
├── netflix_titles_cleaned.csv
├── cleaning_script.py
└── README.md


---

2. cleaning_script.py (Python code used to clean the file)

import pandas as pd

# Load the data
df = pd.read_csv("netflix_titles.csv")

# Remove duplicates
df.drop_duplicates(inplace=True)

# Fill missing values
df['director'].fillna('Unknown', inplace=True)
df['cast'].fillna('Not Available', inplace=True)
df['country'].fillna('Unknown', inplace=True)
df['date_added'].fillna('01 January 1900', inplace=True)
df['rating'].fillna('Not Rated', inplace=True)

# Standardize text formats
df['country'] = df['country'].str.strip().str.title()
df['rating'] = df['rating'].str.strip().str.upper()
df['type'] = df['type'].str.strip().str.title()

# Convert date format
df['date_added'] = pd.to_datetime(df['date_added'], errors='coerce').dt.strftime('%d-%m-%Y')

# Rename columns
df.columns = [col.lower().replace(' ', '_') for col in df.columns]

# Split duration
df['duration_extracted'] = df['duration'].str.extract(r'(\d+)').astype('float')
df['duration_unit'] = df['duration'].str.extract(r'([a-zA-Z]+)').fillna('')

# Save cleaned file
df.to_csv("netflix_titles_cleaned.csv", index=False)


---

3. README.md

# Netflix Dataset Cleaning – Task 1

## Objective
Clean and preprocess raw Netflix dataset to fix common data quality issues.

## Changes Made

- Removed duplicate rows
- Filled missing values in director, cast, country, rating, and date_added
- Standardized case formatting for text columns
- Converted date_added to dd-mm-yyyy format
- Renamed all columns to lowercase with underscores
- Split duration into numeric (duration_extracted) and unit (duration_unit)

## Files

- netflix_titles_cleaned.csv – Final cleaned dataset
- cleaning_script.py – Python code used to clean the data
- README.md – Summary of the cleaning process


---

4. Uploading to GitHub (Mobile Guide)

1. Open GitHub in your browser or use the GitHub app.


2. Create a new repository:
Name it something like netflix-data-cleaning.


3. Upload:

netflix_titles_cleaned.csv (from our previous download)

Copy-paste the cleaning_script.py and README.md using "Add file > Create new file"
