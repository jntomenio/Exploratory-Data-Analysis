[![Up to Date](https://github.com/ikatyang/emoji-cheat-sheet/workflows/Up%20to%20Date/badge.svg)](https://github.com/ikatyang/emoji-cheat-sheet/actions?query=workflow%3A%22Up+to+Date%22)

# ⋆⋆✮♪♫ Exploratory Data Analysis 🎧 Spotify 2023 Dataset ♫♪✮⋆⋆
https://github.com/user-attachments/assets/5cc40d0e-50d6-4145-bb8c-65798c47688b

<!-- ![Build Status](https://travis-ci.org/yourusername/yourproject.svg?branch=main) -->

# :bookmark_tabs: Exploratory Data Analysis

> [!NOTE]
> :open_book: *Exploratory data analysis (EDA)* - is used by data scientists to analyze and investigate data sets and summarize their main characteristics, often employing data visualization methods.[^1] This repository incorporates Python code to decipher two programming problems titled: **Normalization** and **Divisible By 3**.

[^1]: IBM (2020). What Is Exploratory Data Analysis? | IBM. Retrieved from https://www.ibm.com/topics/exploratory-data-analysis

---
<a name="intro"></a>
## 📖 Introduction 
This project offers an exploratory data analysis (EDA) of the Most Streamed Spotify Songs of 2023 dataset, focusing on trends, patterns, and insights in popular music streaming. Using Python and popular data visualization libraries such as Matplotlib and Seaborn, the analysis examines the characteristics of the top-streamed tracks, trends among artists, and the distribution of genres to uncover the critical factors behind this year's biggest hits. This repository includes all the code, visualizations, and insights necessary to understand the evolving dynamics of the music streaming landscape.

> [!IMPORTANT]
> 💡 The analysis was conducted on the dataset available on [Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023). You can download the dataset by clicking the highlighted text for reference.

---
<a name="table"></a>
## 🗂 Table of Contents
- [📖 Introduction](#intro)
- [🗂 Table of Contents](#table)
- [🖥 Overview of Dataset](#over)
  - [📂 How many rows and columns does the dataset contain?](#row+col)
  - [🔢 The data types of each column?](#dtype)
- [📈 Basic Descriptive Statistics](#bstats)
  - [🧮 STREAM STATISTICS: Mean, Median, and Standard Deviation](#mmsd)
  - [📅 Released Year and Artist Count Distribution Statistics](#ryear)
- [🏆 Top Performers](#tp)
  - [🏅 Top 5 Songs in Spotify (2023)](#5t)
  - [🎖️ Top 5 Most Frequent Artist](#5f)
- [🎺 Temporal Trends](#tempo)
  - [📰 Yearly Tracks](#numt)
  - [🕓 Monthly Patterns](#patterns)
- [🎸 Genre and Music Characteristics](#genre)
  - [🔀 Streams and Attributes Correlation](#coor1)
  - [⚛ Attributes Correlation](#coor2)
- [🧿 Platform Popularity](#plat)
  - [📼 Platform Comparison](#pc)
- [💡 Advance Analysis](#adv)
  - [🎹 Keys Distribution](#key)
  - [📣 Top 10 Most Frequent Artists on Charts](#fc)
- [📜 Conclusion](conclu)
- [🔰 Author](#auth)
- [📚 Reference](#ref)


---

<a name="over"></a>
## 🖥 Overview of Dataset
> [!TIP]
> :floppy_disk: Must save the excel file first `spotify2023.csv` (depends how you want to format your filename).

❗ Importing these libraries is essential for data analysis and visualizations

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from math import *
```

##### :keyboard: *Input:*
```python
# Load the CSV file into a DataFrame with a specified encoding since there are special characters
spotify = pd.read_csv('spotify2023.csv', encoding='ISO-8859-1')  # Changed encoding to handle special characters
spotify
```

> [!NOTE] 
> The ***ISO-8859-1*** encoding, also known as *Latin-1*, is a single-byte character encoding that can represent the first 256 Unicode characters. While it is efficient for Western European languages, it has limitations in terms of character representation, especially for languages with special characters or non-Latin scripts.


##### :white_check_mark: *Expected Output:*
<img width="898" alt="Screenshot 2024-11-09 at 18 14 04" src="https://github.com/user-attachments/assets/05550abf-d906-42d1-8302-5fe51c997eba">

<a name="row+col"></a>
### 📂 *How many rows and columns does the dataset contain?*
##### :keyboard: *Input:*
```python
# # To check the number of rows and columns in DataFrame
num_rows, num_columns = spotify.shape

# Display the results
print(f'The DataFrame has {num_rows} rows and {num_columns} columns.')
```

<a name="dtype"></a>
### 🔢 *The data types of each column?*
- Are there any missing values?
##### :keyboard: *Input:*
```python
# Check data types of each column
data_type = spotify.dtypes

print("Data Types of Each Column:\n", data_type)
```

```
# Check for missing values in each column
missing_value = spotify.isnull().sum()

print("Missing Values in Each Column:\n", missing_value)
##### :heavy_check_mark: *One of the Expected Input (random numbers):*
```

##### :white_check_mark: *Expected Outputs:*
<img width="1116" alt="Screenshot 2024-11-09 at 18 32 45" src="https://github.com/user-attachments/assets/0e2beff7-968c-44ef-ba68-af43816dfbde">

---
<a name="bstats"></a>
## 📈 Basic Descriptive Statistics
> [!TIP]
> View the Full Detailed Statistics Values of DataFrame

```python
# OPTIONAL: The statistics of each column (Statistics Values of DataFrame)
spotify.describe() # 'Streams' column is not included
```

<a name="mmsd"></a>
### 🧮 *Mean, Median, and Standard Deviation of the Dataset*
##### :keyboard: *Input:*
```python
# Optionally, to check and if ever there are missing values
spotify['streams'] = spotify['streams'].dropna()  # or fillna(0)

# Convert 'streams' column to numeric, coercing errors to NaN
spotify['streams'] = pd.to_numeric(spotify['streams'], errors='coerce')

# Optionally, drop NaN values if you want to exclude them from calculations
spotify = spotify.dropna(subset=['streams'])
```

```python
# Calculate mean, median, and standard deviation for the 'streams' column
mean_streams = spotify['streams'].mean()
median_streams = spotify['streams'].median()
std_streams = spotify['streams'].std()

print("Stream Stats:\n")
print('Mean: ', mean_streams)
print('Median: ', median_streams)
print('Standard Deviation: ', std_streams)
```

##### :white_check_mark: *Expected Output:*

<img width="326" alt="Screenshot 2024-11-09 at 18 41 20" src="https://github.com/user-attachments/assets/06bfa629-6499-4ba3-b937-09507f0fb08e">


> [!NOTE] 
> - **dropna()** removes rows or columns that contain NaN values, which can be useful when you want to clean your dataset by eliminating incomplete entries.
> - **fillna()** allows you to replace NaN values with a specified value or method, which is helpful when you want to retain the structure of your dataset while addressing missing data.

<a name="ryear"></a>
### 📅 *The distribution of released_year and artist_count.*
- Are there any noticeable trends or outliers?
##### :keyboard: *Input:*
```python
# Count occurrences of each release year
year_count = spotify['released_year'].value_counts().sort_index()
artist_count = spotify['artist_count'].value_counts().sort_index()

# Plotting the distribution of released_year
plt.figure(figsize=(10, 5))
year_count.plot(kind='bar', color='skyblue')
plt.title('Distribution of Tracks by Released Year') 
plt.xlabel('Released Year')
plt.ylabel('# of Tracks') 
plt.show()
```

```python
# Plotting the distribution of artist_count
plt. figure(figsize=(10, 6))
artist_count.plot(kind='bar',color='teal')
plt. title('Distribution of Tracks by Artist Count') 
plt.xlabel('Artist Count')
plt.ylabel('# of Tracks')
plt.show()
```

##### :white_check_mark: *Expected Outputs:*
<img width="912" alt="Screenshot 2024-11-09 at 18 44 56" src="https://github.com/user-attachments/assets/b616da3f-4bf6-41fa-b838-577abea37fe9">
<img width="869" alt="Screenshot 2024-11-09 at 18 45 19" src="https://github.com/user-attachments/assets/fa570536-b138-4d86-a683-05842ecbf66d">

--- 

<a name="tp"></a>
## 🏆 Top Performers
> [!TIP]
> Used pandas, matplotlib library.

```python
# OPTIONAL: The statistics of each column (Statistics Values of DataFrame)
spotify.describe() # 'Streams' column is not included
```
<a name="5t"></a>
### 🏅 *Which track has the highest number of streams? Display the top 5 most streamed tracks.*
##### :keyboard: *Input:*
```python
# Convert the 'streams' column to string type first
spotify['streams'] = spotify['streams'].astype(str)

# Now convert the 'streams' column to numeric after removing commas
spotify['streams'] = pd.to_numeric(spotify['streams'].str.replace(',', '', regex=True), errors='coerce')

# Find the top 5 most streamed tracks
top_tracks = spotify.nlargest(5, 'streams').reset_index(drop=True)

# Display the top 5 most streamed tracks
top_tracks
```
 

##### :white_check_mark: *Expected Output:*
<img width="894" alt="Screenshot 2024-11-09 at 18 50 50" src="https://github.com/user-attachments/assets/f3dd2ce1-b203-4db3-bde0-16366203403d">

<a name="5f"></a>
### 🎖️ *Who are the top 5 most frequent artists based on the number of tracks in the dataset?*
##### :keyboard: *Input:*
```python
# Count the number of tracks for each artist
artist_counts = spotify['artist(s)_name'].str.split(', ').explode().value_counts()

# Get the top 5 most frequent artists
top_artists = artist_counts.nlargest(5).reset_index()

# Display the top 5 most frequent artists
top_artists.columns = ['Artist', 'Track Count']

top_artists
```

##### :white_check_mark: *Expected Outputs:*
<img width="235" alt="Screenshot 2024-11-09 at 18 53 07" src="https://github.com/user-attachments/assets/813dc6cc-6e54-4617-97e1-9a78fe65ebfe">

---
<a name="tempo"></a>
## 🎺 Temporal Trends
```python
# OPTIONAL: The statistics of each column (Statistics Values of DataFrame)
spotify.describe() # 'Streams' column is not included
```
<a name="numt"></a>
### 📰 *Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year.*
##### :keyboard: *Input:*
```python
# Count the number of tracks released per year
tracks_per_year = spotify['released_year'].value_counts().sort_index()

# Plotting the number of tracks released per year
plt.figure(figsize=(10, 6))
tracks_per_year.plot(kind='bar', color='skyblue')
plt.title('Number of Tracks Released Per Year')
plt.xlabel('Year')
plt.ylabel('Number of Tracks')
plt.xticks(rotation=45)
plt.grid(axis='y')
plt.tight_layout()
plt.show()

# Identify the year with the most releases
most_releases_year = tracks_per_year.idxmax()
most_releases_count = tracks_per_year.max()

print(f"The year with the most releases is: {most_releases_year} with {most_releases_count} releases.")
```


##### :white_check_mark: *Expected Output:*
<img width="890" alt="Screenshot 2024-11-09 at 19 12 20" src="https://github.com/user-attachments/assets/250e2de0-549c-402d-88ae-ab5a1d29c1ec">


<a name="patterns"></a>
### 🕓 *Does the number of tracks released per month follow any noticeable patterns?* 
- Which month sees the most releases?
##### :keyboard: *Input:*
```python
import calendar

# Count the number of tracks released per month
tracks_per_month = spotify['released_month'].value_counts().sort_index()

# Plotting the number of tracks released per month
plt.figure(figsize=(10, 6))
bars = tracks_per_month.plot(kind='bar', color='lightblue')
plt.title('Number of Tracks Released Per Month')
plt.xlabel('Month')
plt.ylabel('Number of Tracks')
plt.xticks(ticks=range(12), labels=calendar.month_abbr[1:], rotation=45)  # Use abbreviated month names
plt.grid(axis='y')

# OPTIONAL: For precise data chart, adding values on top of each bar
for bar in bars.patches:
    plt.text(bar.get_x() + bar.get_width() / 2, bar.get_height(), 
             int(bar.get_height()), ha='center', va='bottom')  # Adjust text position

plt.tight_layout()
plt.show()

# Identify the month with the most releases
most_releases_month = tracks_per_month.idxmax()
most_releases_count = tracks_per_month.max()

# Convert the month number to the month name
most_releases_month_name = calendar.month_name[most_releases_month]

print(f"The month with the most releases is: {most_releases_month_name} with {most_releases_count} releases.")
```

##### :white_check_mark: *Expected Outputs:*
<img width="890" alt="Screenshot 2024-11-09 at 18 59 52" src="https://github.com/user-attachments/assets/388d6793-b041-402f-a59b-26fbb8ec8ca3">

---

<a name="genre"></a>
## 🎸 Genre and Music Characteristics
```python
# OPTIONAL: The statistics of each column (Statistics Values of DataFrame)
spotify.describe() # 'Streams' column is not included
```
<a name="coor1"></a>
### 🔀 *Examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. Which attributes seem to influence streams the most?*
##### :keyboard: *Input:*
```python
# Define the columns to convert to numeric
columns_to_convert = ['streams', 'bpm', 'danceability_%', 'energy_%', 'valence_%', 'acousticness_%']

# Convert relevant columns to numeric, forcing errors to NaN
spotify[columns_to_convert] = spotify[columns_to_convert].apply(pd.to_numeric, errors='coerce')

# Calculate the correlation matrix for the relevant attributes
correlation_matrix = spotify[columns_to_convert].corr()
```

```python
# Visualize the correlation using a heatmap
plt.figure(figsize=(10, 8))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', fmt=".3f", square=True, 
            linewidths=0.5, linecolor="black", annot_kws={"size": 12}, cbar_kws={"shrink": .8})

# Adjust ticks and title
plt.xticks(rotation=15, fontsize=10)
plt.yticks(rotation=0, fontsize=10)
plt.title('Correlation between Streams and Musical Attributes', fontsize=16, fontweight='bold')
plt.show()
```

##### :white_check_mark: *Expected Output:*
<img width="880" alt="Screenshot 2024-11-09 at 19 07 34" src="https://github.com/user-attachments/assets/4fc6c946-3729-42a7-8a8d-de470c37b56b">

> [!IMPORTANT]
> - In the heatmap that was constructed almost every attributes has negative correlation when its related to streams, meaning, characteristics has nothing to do with popularity because of the difference of preferences by other people

##### :keyboard: *Input:*
```python
# Define the attributes to plot against streams
attributes = ['danceability_%', 'bpm', 'energy_%', 'valence_%']
titles = ["Streams vs Danceability %", "Streams vs BPM", "Streams vs Energy %", "Streams vs Valence %"]

# Create scatter plots
fig, axes = plt.subplots(1, 4, figsize=(24, 5))

for ax, attr, title in zip(axes, attributes, titles):
    sns.scatterplot(ax=ax, x=attr, y='streams', data=spotify)
    ax.set_title(title)

plt.tight_layout()
plt.show()
```
##### :white_check_mark: *Expected Output:*
<img width="900" alt="Screenshot 2024-11-09 at 19 17 29" src="https://github.com/user-attachments/assets/a2876078-7354-4390-8ff2-a9dee594dc1f">

<a name="coor2"></a>
### ⚛ *Is there a correlation between danceability_% and energy_%? How about valence_% and acousticness_%?*
##### :keyboard: *Input:*
```python
# Calculate correlation coefficients
dance_energy_corr = spotify['danceability_%'].corr(spotify['energy_%'])
valence_acousticness_corr = spotify['valence_%'].corr(spotify['acousticness_%'])

# Plot the values for Visualization
plt.figure(figsize=(12, 5))

# Scatter plot for Danceability vs Energy
plt.subplot(1, 2, 1)
sns.scatterplot(x='danceability_%', y='energy_%', data=spotify)
plt.title('Danceability vs Energy')

# Scatter plot for Valence vs Acousticness
plt.subplot(1, 2, 2)
sns.scatterplot(x='valence_%', y='acousticness_%', data=spotify)
plt.title('Valence vs Acousticness')

plt.tight_layout()
plt.show()

# OPTIONAL: For a definite answer
print(f"Correlation between Danceability and Energy: {dance_energy_corr:}")
print(f"Correlation between Valence and Acousticness: {valence_acousticness_corr:}")
```

##### :white_check_mark: *Expected Outputs:*
<img width="887" alt="Screenshot 2024-11-09 at 19 18 20" src="https://github.com/user-attachments/assets/07a3c398-48b2-42ed-81f2-e948db5a2821">

---

<a name="plat"></a>
## 🧿 Platform Popularity
> [!TIP]
> Used numpy, pandas, seaborn, matplotlib library.

```python
# OPTIONAL: The statistics of each column (Statistics Values of DataFrame)
spotify.describe() # 'Streams' column is not included
```

<a name="pc"></a>
### 📼 *How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare? Which platform seems to favor the most popular tracks?*
##### :keyboard: *Input:*
```python
# Count the number of unique tracks in each dataset
num_tracks_spotify_playlists = spotify[['in_spotify_playlists', 'in_deezer_playlists', 'in_apple_playlists']]

# Create a summary DataFrame
track_counts = pd.DataFrame({
    'Platform': ['Spotify Playlist', 'Deezer Playlist', 'Apple Playlist'],
    # Use .sum(axis=1) to get a 1-dimensional array of total unique tracks for each platform
    'Number of Tracks': num_tracks_spotify_playlists.sum(axis=0).values  # Corrected to sum across columns
})

most_releases_platforms = track_counts['Platform'].max()
most_releases_count = track_counts['Number of Tracks'].max()  # Corrected column name to match

track_counts
```


##### :white_check_mark: *Expected Output:*
<img width="262" alt="Screenshot 2024-11-09 at 19 23 20" src="https://github.com/user-attachments/assets/bd5a1c9d-86d8-4b31-ac0c-c6965a3b09cc">

---

<a name="adv"></a>
## 💡 Advance Analysis
> [!TIP]
> Used numpy, pandas, matplotlib library.

```python
# OPTIONAL: The statistics of each column (Statistics Values of DataFrame)
spotify.describe() # 'Streams' column is not included
```

<a name="key"></a>
### 🎹 *Based on the streams data, can you identify any patterns among tracks with the same key or mode (Major vs. Minor)?*
##### :keyboard: *Input:*
```python
# Calculate counts for each combination of key and mode
key_mode_counts = spotify.groupby(['key', 'mode']).size().unstack(fill_value=0)

# Define custom colors
colors = {'Major': 'lightblue', 'Minor': 'yellowgreen'}

# Plotting
plt.figure(figsize=(12, 8))

# Create bar positions
bar_width = 0.35
x = range(len(key_mode_counts))

# Create bars for each mode
for i, mode in enumerate(key_mode_counts.columns):
    plt.bar(
        [pos + i * bar_width for pos in x], 
        key_mode_counts[mode], 
        width=bar_width, 
        label=mode, 
        color=colors[mode]
    )

# OPTIONAL: For precise data, putting value labels
for i, mode in enumerate(key_mode_counts.columns):
    for j, count in enumerate(key_mode_counts[mode]):
        plt.text(
            j + i * bar_width, 
            count, 
            str(count), 
            ha='center', 
            va='bottom', 
            fontsize=10
        )

plt.title('Distribution of Tracks by Key and Mode', fontsize=16, fontweight='bold')
plt.xlabel('Key', fontsize=14)
plt.ylabel('Number of Tracks', fontsize=14)
plt.xticks([pos + bar_width / 2 for pos in x], key_mode_counts.index, rotation=45)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.legend(title='Mode', title_fontsize='13', fontsize='11')
plt.tight_layout()  # Adjust layout to make room for labels
plt.show()
```


##### :white_check_mark: *Expected Output:*
<img width="884" alt="Screenshot 2024-11-09 at 19 26 18" src="https://github.com/user-attachments/assets/c7664a14-8eb1-4b26-a0e5-dafe98b6ed8c">

<a name="fc"></a>
### 📣 *Do certain genres or artists consistently appear in more playlists or charts?*
- Perform an analysis to compare the most frequently appearing artists in playlists or charts.
##### :keyboard: *Input:*
```python
# Count the occurrences of each artist across all relevant columns
platform_columns = [
    'in_spotify_playlists', 
    'in_spotify_charts', 
    'in_apple_playlists', 
    'in_apple_charts', 
    'in_deezer_playlists', 
    'in_deezer_charts'
]

# Convert relevant columns to numeric and fill NaNs with 0 in one step
spotify[platform_columns] = spotify[platform_columns].apply(pd.to_numeric, errors='coerce').fillna(0)

# Group by artist and sum the occurrences across all relevant columns
artist_counts = spotify.groupby("artist(s)_name")[platform_columns].agg('sum').sum(axis=1).nlargest(10).reset_index()

# Rename columns for clarity
artist_counts.columns = ['Artist', 'Appearances']

# Generate a pastel color palette
pastel_colors = sns.color_palette("pastel", n_colors=len(artist_counts))

# Plotting
plt.figure(figsize=(14, 7))
plt.barh(artist_counts['Artist'], artist_counts['Appearances'], color=pastel_colors)

plt.title('Top 10 Most Frequently Appearing Artists in Playlists/Charts', fontsize=16, fontweight='bold')
plt.xlabel('Appearances in Playlists/Charts', fontsize=14)
plt.ylabel('Artist', fontsize=14)
plt.grid(axis='x', linestyle='--', alpha=0.7)

plt.show()
```

##### :white_check_mark: *Expected Outputs:*
<img width="895" alt="Screenshot 2024-11-09 at 19 28 12" src="https://github.com/user-attachments/assets/78997391-0348-476a-84f8-f12823919233">

#### The Top 3 Artists frequently appearing in playlist and charts are The Weeknd, Taylor Swift, and Ed Sheeran. They are known for their Pop, Romance, and RnB songs

---
<a name="conclu"></a>
## 📜 Conclusion

This EDA provides valuable insights into Spotify's 2023 music landscape, identifying factors that may impact track popularity and trends in music releases. Further analysis could focus on examining correlations between additional attributes or investigating playlist curation criteria.

---
<a name="auth"></a>
## 🔰 Author
Julian Bernice Kristoffer Tomenio

<a name="ref"></a>
## 📚 References
- https://github.com/eli64s/readme-ai.git

