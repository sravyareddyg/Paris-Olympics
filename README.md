# Analyzing the Paris 2024 Olympic Dataset with Python and Power BI.
### Dashboard Link : https://app.powerbi.com/view?r=eyJrIjoiODZlZDEwN2YtYTcwZS00MjVlLTkyNzItOWFiNDJlYzk1MDRmIiwidCI6ImRmODY3OWNkLWE4MGUtNDVkOC05OWFjLWM4M2VkN2ZmOTVhMCJ9
## Introduction
 The Paris 2024 Summer Olympics promise to be a grand event, and analyzing the related datasets can provide valuable insights into various aspects of the games. This project explores how to use Python to download and manage the dataset from Kaggle, and then utilize Power BI to visualize the insights for effective analysis.
## Table of Contents
- Introduction
- Getting Started
    - Prerequisites
    - Setting Up Kaggle API
    - Python Environment Setup
- Downloading the Dataset
- Preparing Data for Visualization
- Importing Data into Power BI
- Creating Visualizations in Power BI
- Conclusion
- Further Exploration
## Getting Started
### Prerequisites
  - Python 3.x
  - Kaggle account
  - Power BI Desktop
### Setting Up Kaggle API
**1. Sign up on Kaggle:** If you don’t have a Kaggle account, sign up  [here](https://www.kaggle.com/account/login).

**2.Create an API Token:** In your Kaggle account settings, go to the “API” section and click “Create New API Token.” This will download a kaggle.json file containing your credentials.

**3.Save the API Token:** Place the kaggle.json file in a secure directory on your machine, where it will be used to authenticate the Kaggle API.
### Python Environment Setup
Make sure you have Python installed along with the necessary libraries:

    pip install kaggle pandas
### Downloading the Dataset
Below is the Python script that automates the process of downloading the Paris 2024 Olympic dataset from Kaggle and loading it into Pandas DataFrames for analysis.
    
      import kaggle
      import os
      import pandas as pd
      # Set Kaggle API credentials directory
      os.environ['KAGGLE_CONFIG_DIR'] = 'C:/Users/yourusername/.kaggle'  # Update this path to your Kaggle configuration directory
      # Specify the dataset identifier
      dataset = 'piterfm/paris-2024-olympic-summer-games'
      # Set the download path
      download_path = 'C:/Users/yourusername/Downloads/OlympicData'  # Change this to your preferred download directory
      # Remove existing files in the folder to prevent duplicates or outdated files
      for file in os.listdir(download_path):
      file_path = os.path.join(download_path, file)
      try:
        if os.path.isfile(file_path):
            os.unlink(file_path)  # Delete the file
            print(f"Deleted {file_path}")
    except Exception as e:
        print(f"Error deleting {file_path}: {e}")

    # Download the dataset using the Kaggle API and unzip the files
    kaggle.api.dataset_download_files(dataset, path=download_path, unzip=True)
    # List of CSV files to be imported
    csv_files = [
    'athletes.csv',
    'events.csv',
    'medallists.csv',
    'medals.csv',
    'medals_total.csv',
    'schedules.csv',
    'schedules_preliminary.csv',
    'teams.csv',
    'torch_route.csv',
    'venues.csv'
      ]

    # Initialize a dictionary to hold DataFrames
    dataframes = {}

    # Iterate through each CSV file and load it into a DataFrame
    for file in csv_files:
    # Construct the full path to the CSV file
    file_path = os.path.join(download_path, file)
    
    # Load the CSV file into a Pandas DataFrame
    df = pd.read_csv(file_path)
    
    # Add the DataFrame to the dictionary using the file name as the key
    table_name = file.split('.')[0]  # Remove the .csv extension
    dataframes[table_name] = df'
### Preparing Data for Visualization
This script downloads and prepares the dataset for analysis by:

**1.Setting the Environment:** Configuring the Kaggle API credentials.

**2.Dataset Identifier:** Specifying the dataset to download.

**3.Clearing Existing Files:** Removing outdated or duplicate files in the download directory.

**4.Downloading and Unzipping:** Downloading the dataset and unzipping the files.

**5.Loading CSV Files into DataFrames:** Loading each CSV file into a Pandas DataFrame and storing them in a dictionary.

## Importing Data into Power BI

With the dataset downloaded and organized into DataFrames, we can now import this data into Power BI for visualization.

### Connecting Power BI to Python
1. **Open Power BI:** Start by opening Power BI Desktop.
   
2. **Get Data:** Click on “Get Data” in the Home tab and choose “Python script” as the data source.
   
3. **Load the Script:** Copy and paste the following Python script into the Power BI editor to load the DataFrames:
   
        import pandas as pd
        import os

        # Define the path to the downloaded CSV files  
        download_path = 'C:/Users/yourusername/Downloads/OlympicData'

        # Load the data into DataFrames
        athletes = pd.read_csv(os.path.join(download_path, 'athletes.csv'))
        events = pd.read_csv(os.path.join(download_path, 'events.csv'))
        medallists = pd.read_csv(os.path.join(download_path, 'medallists.csv'))
        medals = pd.read_csv(os.path.join(download_path, 'medals.csv'))
        medals_total = pd.read_csv(os.path.join(download_path, 'medals_total.csv'))
        schedules = pd.read_csv(os.path.join(download_path, 'schedules.csv'))
        schedules_preliminary = pd.read_csv(os.path.join(download_path, 'schedules_preliminary.csv'))
        teams = pd.read_csv(os.path.join(download_path, 'teams.csv'))
        torch_route = pd.read_csv(os.path.join(download_path, 'torch_route.csv'))
        venues = pd.read_csv(os.path.join(download_path, 'venues.csv'))
4. **Load the Data:** Once the script is executed, Power BI will load the data from the CSV files into tables that can be used for building reports.
## Creating Visualizations in Power BI

With the data loaded into Power BI, we can now create compelling visualizations to analyze the Olympic dataset. Here are a few examples:

### Visual 1: Athlete Participation by Country

Type: Bar Chart

Fields: Use the athletes table to plot the number of athletes participating from each country.

### Visual 2: Medal Count by Country

Type: Pie Chart

Fields: Utilize the medals_total table to display the total medal count for each country.

### Visual 3: Event Schedule

Type: Table

Fields: Use the schedules table to create a detailed schedule of events, including event names, dates, and venues.

### Visual 4: Torch Route Map

Type: Map

Fields: Employ the torch_route table to visualize the Olympic torch route on a map.

### Visual 5: Medal Trends Over Time

Type: Line Chart

Fields: Use the medals table to display trends in medal wins over time, broken down by country or sport.

## Conclusion

By leveraging Python and Power BI, we’ve efficiently downloaded, organized, and visualized the Paris 2024 Olympic dataset. This project demonstrates the power of data analysis and visualization in understanding the dynamics of a global event like the Olympics.

Through this exploration, we gain valuable insights into athlete participation, medal trends, event schedules, and more. As the 2024 Summer Olympics draw nearer, this analysis provides a fascinating glimpse into the event’s potential outcomes and highlights the immense scale and diversity of the games.

## Further Exploration
**Advanced Analytics:** Dive deeper into advanced analytics by applying machine learning models to predict medal outcomes or identify key performance indicators for athletes.
**Dynamic Dashboards:** Enhance Power BI reports with dynamic dashboards, providing interactive and real-time updates on Olympic events and statistics
  
