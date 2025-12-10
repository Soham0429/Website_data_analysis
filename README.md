# Website Data Analysis

## Overview
This project performs an exploratory data analysis (EDA) on website traffic data to understand user behavior, traffic patterns, and engagement trends over time.

## Technologies Used
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn

## Dataset
The dataset contains website traffic metrics such as sessions, users, and date-time information.

---

## Import Libraries
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

## Load Dataset
```python
df = pd.read_csv("website_data.csv")
df
```

## Initial Data Exploration
```python
df.head()
```

```python
df.info()
```

```python
df.describe()
```

```python
df.columns
```

```python
df.isnull().sum()
```

---

## Date-Time Feature Engineering
```python
df["DateHour"] = pd.to_datetime(df["DateHour"])

df["Hour"] = df["DateHour"].dt.hour
df["Day"] = df["DateHour"].dt.day
df["Month"] = df["DateHour"].dt.month
df["Weekday"] = df["DateHour"].dt.day_name()

df.head()
```

---

## Sessions Over Time
```python
plt.figure(figsize=(10,5))
sns.lineplot(data=df, x="DateHour", y="Sessions")
plt.title("Sessions Over Time")
plt.show()
```

---

## Users Over Time
```python
plt.figure(figsize=(10,5))
sns.lineplot(data=df, x="DateHour", y="Users")
plt.title("Users Over Time")
plt.show()
```

---

## Sessions by Hour
```python
plt.figure(figsize=(10,5))
sns.barplot(data=df, x="Hour", y="Sessions")
plt.title("Sessions by Hour")
plt.show()
```

---

## Sessions by Weekday
```python
plt.figure(figsize=(10,5))
sns.barplot(data=df, x="Weekday", y="Sessions")
plt.title("Sessions by Weekday")
plt.xticks(rotation=45)
plt.show()
```

---

## Average Sessions and Users by Weekday
```python
df.groupby("Weekday")[["Sessions","Users"]].mean()
```

---

## Average Sessions and Users by Hour
```python
df.groupby("Hour")[["Sessions","Users"]].mean()
```

---

## Pivot Table for Heatmap
```python
pivot_table = df.pivot_table(
    values="Sessions",
    index="Weekday",
    columns="Hour",
    aggfunc="mean"
)

pivot_table
```

---

## Heatmap of Average Sessions
```python
plt.figure(figsize=(12,6))
sns.heatmap(pivot_table, cmap="Blues")
plt.title("Heatmap of Average Sessions")
plt.show()
```

---

## Sessions per User
```python
df["Sessions_per_User"] = df["Sessions"] / df["Users"]
df.head()
```

---

## Top 10 Records by Sessions
```python
df.sort_values(by="Sessions", ascending=False).head(10)
```

---

## Top 10 Records by Users
```python
df.sort_values(by="Users", ascending=False).head(10)
```

---

## Overall Sessions and Users Trend
```python
df.groupby("DateHour")[["Sessions","Users"]].sum().plot(figsize=(12,6))
plt.title("Sessions and Users Over Time")
plt.show()
```

---

## Key Takeaways
- Website traffic varies significantly by hour and weekday.
- Certain time periods show peak engagement.
- Sessions per user metric helps identify engagement quality.

## Conclusion
This analysis helps in understanding website performance trends and can be further extended with predictive modeling or user segmentation.
