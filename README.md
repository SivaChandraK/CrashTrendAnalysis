
# Crash Trends Analysis

This project analyzes crash trends based on a dataset capturing details about crashes, including time, location, vehicle involvement, demographics, and holiday periods. The analysis uses Python with libraries such as pandas and matplotlib for data processing and visualization.

## Key Features

1. **Data Cleaning**
   - Removed columns with excessive missing data.
   - Handled missing values for critical attributes (e.g., `Time`, `Crash Type`).
   - Filtered out invalid or unspecified values for attributes like `Gender` and `Age`.

2. **Exploratory Data Analysis (EDA)**
   - Crash trends by **year, month, day of the week, and time of day**.
   - Distribution of crashes by **gender** and **age groups**.
   - Impact of **vehicle types** and **speed limits** on crash severity.
   - Seasonal and holiday-period crash trends.

3. **Insights Generation**
   - Proportion of crashes during holiday periods.
   - Correlation of crash severity with factors like speed limits, vehicle types, and road users.

## Visualizations

### 1. Crash Trends by Gender (Excluding Unspecified)
A pie chart illustrating the proportion of crashes involving males and females:

```python
import matplotlib.pyplot as plt

# Filter out 'Unspecified' from Gender
filtered_gender_data = cleaned_data[cleaned_data['Gender'].isin(['Male', 'Female'])]

# Count crashes by gender
crashes_by_gender = filtered_gender_data['Gender'].value_counts()

# Plot pie chart
plt.figure(figsize=(8, 8))
crashes_by_gender.plot(
    kind='pie', 
    autopct='%1.1f%%', 
    colors=['lightblue', 'pink'], 
    startangle=90
)
plt.title('Crash Trends by Gender (Excluding Unspecified)')
plt.ylabel('')
plt.show()
```

### 2. Crash Trends by Season
Bar chart showing crash distribution across seasons:

```python
# Assign seasons based on months
def assign_season(month):
    if month in [12, 1, 2]:
        return 'Summer'
    elif month in [3, 4, 5]:
        return 'Autumn'
    elif month in [6, 7, 8]:
        return 'Winter'
    else:
        return 'Spring'

cleaned_data['Season'] = cleaned_data['Month'].apply(assign_season)

# Count crashes by season
crashes_by_season = cleaned_data['Season'].value_counts()

# Plot bar chart
plt.figure(figsize=(8, 6))
crashes_by_season.plot(kind='bar', color=['gold', 'brown', 'blue', 'green'])
plt.title('Crash Trends by Season')
plt.xlabel('Season')
plt.ylabel('Number of Crashes')
plt.grid(axis='y')
plt.show()
```

### 3. Vehicle Type Correlation with Crash Severity
Bar chart analyzing crash severity based on vehicle involvement:

```python
# Group by Crash Type and vehicle involvement
vehicle_severity = cleaned_data.groupby(['Crash Type'])[
    ['Bus Involvement', 'Heavy Rigid Truck Involvement', 'Articulated Truck Involvement']
].apply(lambda x: x.apply(lambda y: (y == 'Yes').sum()))

# Plot bar chart
vehicle_severity.T.plot(kind='bar', figsize=(12, 6), stacked=True, color=['skyblue', 'salmon'])
plt.title('Vehicle Type Correlation with Crash Severity')
plt.xlabel('Vehicle Type')
plt.ylabel('Number of Crashes')
plt.legend(title='Crash Type', loc='upper right')
plt.xticks(rotation=0)
plt.grid(axis='y')
plt.show()
```

## Findings

1. **Gender Distribution**
   - Majority of crashes involve males.
   - Excluding unspecified values highlights clear gender-based trends.

2. **Seasonal Trends**
   - Summer has the highest crash counts, while Winter shows fewer crashes.

3. **Vehicle Types**
   - Heavy rigid trucks and articulated trucks are more involved in severe crashes (e.g., multiple-vehicle).

4. **Holiday Periods**
   - Crashes during holiday periods account for 3.6%, consistent with the 3.6% time these periods represent in a year.
     
5. **Age of Driver**
   - Young Drivers (17-25 years): This group has the highest crash involvement due to inexperience and riskier driving behavior.

6. **Speed of Vehicle**
   - Low Speed Limits (20-60 km/h): Crashes in these zones are predominantly single-vehicle, reflecting urban or residential areas.
   - Moderate Speed Limits (70-90 km/h): Both single- and multiple-vehicle crashes occur, typical of arterial roads or semi-rural areas.
   - High Speed Limits (100+ km/h): High-speed crashes are often multiple-vehicle and severe, characteristic of highway conditions.

## Usage

1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/crash-trends-analysis.git
   cd crash-trends-analysis
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Run the analysis:
   ```bash
   python analysis.py
   ```

4. View visualizations:
   Generated plots will be displayed inline or saved to the `output` folder.

## Contributions
Contributions are welcome! Please submit issues or pull requests to suggest improvements.

## License
This project is licensed under the MIT License.
