# **Housing Market Price Prediction**

This project analyzes a real estate dataset to predict property prices based on features like square footage, number of bedrooms, bathrooms, and waterfront views. The project includes **data wrangling**, **exploratory data analysis (EDA)**, and **model development and evaluation**.

## **Project Structure**

### **1. Data Wrangling and Cleaning**
   - Handled missing values by replacing NaNs with the mean value.
   - Conducted preliminary data inspection to ensure data quality.

### **2. Exploratory Data Analysis (EDA)**
   - **Value Counts**: Found that houses with 1.0 floor are the most common (10,680 houses), followed by those with 2 floors (8,241 houses). Only 8 houses have more than 3 floors.
   - **Box Plot (Waterfront vs. Price)**: Analyzed the impact of waterfront views on property prices. Houses without a waterfront view showed more price outliers, whereas houses with a waterfront view generally had higher median prices.
   - **Regression Plot (sqft_above vs. Price)**: Explored the correlation between the square footage above ground and price. A positive correlation indicates that properties with more square footage above ground tend to have higher prices.
   - **Correlation Matrix**:
     - The feature most correlated with price is `sqft_living` (0.702), followed by `grade` (0.667) and `sqft_above` (0.605).
     - Other features, such as `bathrooms` and `sqft_living15`, also show significant correlations with `price`.
     - `zipcode` has a slightly negative correlation with `price`, indicating that ZIP codes might not strongly impact property values in this dataset.
