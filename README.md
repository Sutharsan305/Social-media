# Social-media
Exploratory Data Analysis on YouTube data.
# Import pandas
import pandas as pd
# Read the Dataset
data = pd.read_csv('youtube_dislike_dataset.csv')
# Display top 5 records
data.head(5)
# Display top 5 records
top_5_records = data.head(5)
print("Top 5 records:")
print(top_5_records)
# Display bottom 5 records
data.tail(5)
# Display bottom 5 records
bottom_5_records = data.tail(5)
print("\nBottom 5 records:")
print(bottom_5_records)
# Display information about the dataframe
data.info()
data.shape
# Calculate the percentage of missing values
missing_percent = (data.isnull().sum() / len(data)) * 100
print("Percentage of missing values:")
print(missing_percent)
# Decision: Drop or Impute missing values
# Example: Impute missing values in the 'comments' column with an empty string
data['comments'].fillna('', inplace=True)
# You can choose to drop columns or rows with a certain threshold of missing values
# Example: Drop columns with more than 30% missing values
threshold = 30
data.dropna(axis=1, thresh=len(data) * (1 - threshold / 100), inplace=True)

# Example: Drop rows with missing values
data.dropna(axis=0, inplace=True)

# Display the updated shape of the dataset after dropping or imputing
print("Shape of the dataset after dropping/imputing:", data.shape)

#check the missing value
print((data.isnull().sum() / len(data)) * 100)

# Display statistical summary of numerical columns
numerical_summary = data.describe()

print("Statistical summary of numerical columns:")
print(numerical_summary)

# Display statistical summary of categorical columns
categorical_summary = data.describe(include=['object']).T

print("\nStatistical summary of categorical columns:")
print(categorical_summary)

# Just reference
data.columns

# Convert 'published_at' column to datetime
data['published_at'] = pd.to_datetime(data['published_at'])

# Only Display the updated dataframe
print(data['published_at'])

# Three Display the updated dataframe
print(data.head(3))

# Create a new column 'published_month' with the months
data['published_month'] = data['published_at'].dt.month

# Display the updated dataframe with the months only column
print(data['published_month'])

# Create a new column 'published_month' with the full month names
data['published_month'] = data['published_at'].dt.month

# Define a mapping from month numbers to month names
month_mapping = {
    1: 'Jan', 2: 'Feb', 3: 'Mar', 4: 'Apr', 5: 'May', 6: 'Jun',
    7: 'Jul', 8: 'Aug', 9: 'Sep', 10: 'Oct', 11: 'Nov', 12: 'Dec'
}

# Replace numerical values with month names
data['published_month'] = data['published_month'].apply(lambda x: month_mapping.get(x))

# Display the updated dataframe with month names
print(data['published_month'])

# Find the number of videos published each month and arrange in decreasing order
video_count_per_month = data.groupby(['published_month'])['video_id'].count().sort_values(ascending=False)

# Display the result
print(video_count_per_month)

# Find the count of unique video_id, channel_id, and channel_title
unique_video_id_count = data['video_id'].nunique()
unique_channel_id_count = data['channel_id'].nunique()
unique_channel_title_count = data['channel_title'].nunique()

# Display the counts
print("Count of unique video_id:", unique_video_id_count)
print("Count of unique channel_id:", unique_channel_id_count)
print("Count of unique channel_title:", unique_channel_title_count)

# Find the count of videos for each channel and sort in descending order
channel_video_count = data['channel_title'].value_counts()

# Top 10 channels with the highest number of videos
top_10_channels = channel_video_count.head(10)

# Display the results
print("Top 10 channels with the highest number of videos:")
print(top_10_channels)

# Bottom 10 channels with the lowest number of videos
bottom_10_channels = channel_video_count.tail(10)

print("\nBottom 10 channels with the lowest number of videos:")
print(bottom_10_channels)

# Find the title of the video with the maximum and minimum likes
max_likes_title = data.loc[data['likes'].idxmax(), 'title']
min_likes_title = data.loc[data['likes'].idxmin(), 'title']

# Display the titles
print("Title of the video with the maximum number of likes:", max_likes_title)
print("Title of the video with the minimum number of likes:", min_likes_title)

# Find the title of the video with the maximum and minimum dislikes
max_dislikes_title = data.loc[data['dislikes'].idxmax(), 'title']
min_dislikes_title = data.loc[data['dislikes'].idxmin(), 'title']

# Display the titles
print("Title of the video with the maximum number of dislikes:", max_dislikes_title)
print("Title of the video with the minimum number of dislikes:", min_dislikes_title)

import matplotlib.pyplot as plt
import seaborn as sns 

# Calculate the correlation between 'view_count' and 'dislikes'
correlation = data['view_count'].corr(data['dislikes'])

# Create a scatter plot
plt.figure(figsize=(10, 6))
sns.scatterplot(data=data, x='view_count', y='dislikes', alpha=0.5)
plt.title(f"Scatter Plot of View Count vs Dislikes\nCorrelation: {correlation:.2f}")
plt.xlabel('View Count')
plt.ylabel('Dislikes')
plt.grid(True)
plt.show()

print("Correlation between view_count and dislikes:", correlation)

# Filter videos published in January
videos_january = data[data['published_at'].dt.month == 1]

# Display information about videos published in January
videos_january

  # Convert 'published_at' column to datetime if not done already
data['published_at'] = pd.to_datetime(data['published_at'])

# Count the number of videos published in January
count_january_videos = videos_january.shape[0]
print("Count of videos published in January:", count_january_videos) 

