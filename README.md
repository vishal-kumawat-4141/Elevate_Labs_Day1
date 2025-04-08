import pandas as pd

# Load the dataset
df = pd.read_csv('netflix_titles.csv')

# Step 1: Display missing values
print("Missing values per column:\n", df.isnull().sum())

# Step 2: Handle missing values
df['director'].fillna('Unknown', inplace=True)
df['cast'].fillna('Not Specified', inplace=True)
df['country'].fillna('Unknown', inplace=True)
df['date_added'].fillna(df['date_added'].mode()[0], inplace=True)
df['rating'].fillna(df['rating'].mode()[0], inplace=True)
df['duration'].fillna('Unknown', inplace=True)

# Step 3: Remove duplicate rows
df.drop_duplicates(inplace=True)

# Step 4: Standardize column names
df.columns = df.columns.str.strip().str.lower().str.replace(' ', '_')

# Step 5: Convert date_added to datetime format
df['date_added'] = pd.to_datetime(df['date_added'], errors='coerce')

# Step 6: Save the cleaned dataset
df.to_csv('netflix_titles_cleaned.csv', index=False)

# Step 7: Final check
print("\n✅ Data Cleaning Completed Successfully!")
print("Cleaned dataset saved as: netflix_titles_cleaned.csv")
print("\nUpdated Data Info:")
print(df.info())
