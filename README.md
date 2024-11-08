# *Housing Market Price Prediction*

This project analyzes a real estate dataset to predict property prices based on features like square footage, number of bedrooms, bathrooms, and waterfront views. The project includes **data wrangling**, **exploratory data analysis (EDA)**, and **model development and evaluation**.

## *Project Structure*

## Data Wrangling and Cleaning
   - Handled missing values by replacing NaNs with the mean value.
   - Conducted preliminary data inspection to ensure data quality.

## Exploratory Data Analysis (EDA)
   - **Value Counts**: Found that houses with 1.0 floor are the most common (10,680 houses), followed by those with 2 floors (8,241 houses). Only 8 houses have more than 3 floors.
   - **Box Plot (Waterfront vs. Price)**: Analyzed the impact of waterfront views on property prices. Houses without a waterfront view showed more price outliers, whereas houses with a waterfront view generally had higher median prices.
   - **Regression Plot (sqft_above vs. Price)**: Explored the correlation between the square footage above ground and price. A positive correlation indicates that properties with more square footage above ground tend to have higher prices.
   - **Correlation Matrix**:
     - The feature most correlated with price is `sqft_living` (0.702), followed by `grade` (0.667) and `sqft_above` (0.605).
     - Other features, such as `bathrooms` and `sqft_living15`, also show significant correlations with `price`.
     - `zipcode` has a slightly negative correlation with `price`, indicating that ZIP codes might not strongly impact property values in this dataset.
    
## Initial Feature-by-Feature Model Evaluation

1. **Longitude (R² = 0.00047)**: When I used `longitude` as a single feature, the R² value was extremely low, close to zero. This indicates that `longitude` alone explains almost none of the variance in `price`, suggesting it’s not a useful predictor on its own. While `longitude` might add some value in combination with other features, by itself, it provides very little information.

2. **sqft_living (R² = 0.49285)**: When I used `sqft_living` as the sole feature, the R² value rose to approximately 0.49, meaning that this feature alone explained around 49.3% of the variance in `price`. This makes it a strong predictor, showing that the size of the living area has a significant impact on `price`. `sqft_living` is clearly more relevant for predicting `price` compared to `longitude`.

3. **Multiple Features (R² = 0.6577)**: After combining multiple features, the R² improved to about 0.658, indicating that this set of features collectively explained around 65.8% of the variance in `price`. This result highlights the benefit of using multiple features to capture the various factors affecting `price`, ultimately improving the model’s predictive accuracy.

**Key Insight**: From this initial evaluation, I saw that while some individual features (like `longitude`) offered little predictive power, others (like `sqft_living`) were much more informative. Combining features generally improved the model’s performance, suggesting that multiple aspects contribute to determining `price`.

## Creating a Pipeline with Polynomial Features and Linear Regression

I then created a pipeline with three steps:
1. **StandardScaler**: This step standardized the features by removing the mean and scaling to unit variance, which helps models like linear regression perform better by putting all features on a similar scale.
2. **PolynomialFeatures (degree 2)**: Adding polynomial features allowed the model to capture non-linear relationships between the features and `price` by adding interaction terms and squares of the original features.
3. **LinearRegression**: Finally, I used a linear regression model to fit these transformed features.

- **Pipeline R² = 0.7513**: Using this pipeline, the R² value improved to approximately 0.7513, indicating that the model now explained about 75.1% of the variance in `price`. This improvement in R² shows that incorporating non-linear relationships through polynomial features and scaling helped the model fit the data better.

**Key Insight**: By adding polynomial terms, I allowed the model to capture more complex interactions between the features, which a linear regression model alone would miss. This approach proved to be more effective for complex relationships within the data.

## Model Evaluation and Refinement with Ridge Regression

I split the data into training and test sets to evaluate the model’s generalizability. Here’s a breakdown of the process:

- **Train-Test Split**:
  - Number of training samples: 18,371
  - Number of test samples: 3,242
  - This split allowed me to see how well the model performed on new, unseen data.

- **Ridge Regression with α=0.1 (R² = 0.6536)**:
  - I applied Ridge Regression with a regularization parameter (α) of 0.1. Ridge Regression is a form of linear regression with regularization, which penalizes large coefficients to help prevent overfitting.
  - The R² score for this Ridge Regression model was approximately 0.6536, similar to the original multiple feature model without regularization (R² = 0.6577). This suggests that regularization didn’t improve performance much, meaning the model wasn’t overfitting significantly.

**Key Insight**: Regularization is useful for reducing overfitting, but in this case, the original model was likely not overfitting too much, as indicated by the minimal change in R². Ridge Regression still helped make the model more robust by reducing the influence of less important features.

## Polynomial Transformation with Ridge Regression

Finally, I performed a second-order polynomial transformation on both the training and testing data, then applied Ridge Regression with α=0.1.

- **Second-Order Polynomial with Ridge (R² = 0.7418)**:
  - Using this approach, the R² value improved to approximately 0.7418, indicating that this model explained about 74.2% of the variance in `price`.
  - The improvement in R² compared to the linear Ridge Regression model (R² = 0.6536) shows that the polynomial transformation effectively captured additional non-linear relationships in the data.

**Key Insight**: The polynomial transformation added flexibility to the model, allowing it to capture more complex patterns in the data and improving predictive performance. Ridge regularization helped prevent overfitting by controlling the influence of the polynomial features, resulting in a model that balanced complexity and generalizability.

## **Conclusions**:
   - **Feature Importance**: Some features, like `sqft_living`, were strong predictors of `price`, while others, like `longitude`, had minimal impact. Using multiple relevant features generally resulted in better performance.
   - **Non-Linearity**: Polynomial features allowed the model to capture non-linear relationships, significantly boosting the R² score and enhancing the model’s predictive ability.
   - **Regularization**: Ridge Regression’s regularization helped to make the model more robust. While it didn’t substantially improve the R² here, it was useful in combination with polynomial terms to prevent overfitting.
