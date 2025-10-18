


## **Project Overview**

This study focuses on developing a **machine learning regression model** to **predict delivery time (Time Taken)** for app-based food delivery services.

Delivery speed is a key factor in **customer satisfaction** and a **competitive advantage** for logistics and food delivery companies. Accurate time estimation helps the company to:

* Optimize **courier allocation and delivery routes**,
* Increase **transparency for customers**, and
* Reduce **operational costs due to incorrect estimations**.

A **machine learning approach** was chosen because it can **capture complex, non-linear patterns** in variables affecting delivery time, such as traffic conditions, weather, courier characteristics, and geographic distance. Traditional approaches (e.g., average calculations or simple linear regression) often fail to accurately represent interactions among these variables.

---

#### **Dataset Summary & Exploratory Analysis**

The dataset contains **45,584 observations** covering courier demographics, operational conditions, and geographic factors. Descriptive statistics show delivery times ranging from **10 to 54 minutes**, with an average of **26.29 minutes**.

Key findings from **Exploratory Data Analysis (EDA)**:

| Key Factor               | Category / Value                  | Impact on Delivery Time | Interpretation                                                              |
| ------------------------ | --------------------------------- | ----------------------- | --------------------------------------------------------------------------- |
| **City**                 | Semi-Urban (49 min)               | Very High               | Inefficient infrastructure and routes result in the longest delivery times. |
| **Festival**             | Yes (45 min)                      | High                    | Significant demand surge and congestion.                                    |
| **Road Traffic Density** | Peak (31 min)                     | High                    | Most influential operational factor daily.                                  |
| **Weather Conditions**   | Cloudy/Fog (29 min)               | Medium                  | Adverse weather slows down deliveries.                                      |
| **Type of Vehicle**      | Scooter/Electric Scooter (24 min) | Low                     | More efficient in dense traffic.                                            |
| **Type of Order**        | All categories similar (26 min)   | Neutral                 | Not significant for delivery time.                                          |

**Key insight:** Semi-Urban areas and Festival periods are the most critical factors increasing delivery time, while sunny weather and low traffic contribute to efficiency.

---

#### **Model Performance Summary**

Several models were tested, including **Linear Regression**, **Random Forest**, **CatBoost**, and **XGBRegressor**.

| Model                   | RMSE      | MAE       | MAPE        | Ranking | Notes                                                                |
| ----------------------- | --------- | --------- | ----------- | ------- | -------------------------------------------------------------------- |
| **XGBRegressor (Best)** | **4.775** | **3.765** | **16.803%** | 🥇 1    | Highest accuracy and stable across train, validation, and test sets. |
| CatBoost                | 4.776     | 3.772     | 16.831%     | 🥈 2    | Performance nearly equal to XGB.                                     |
| Random Forest           | 4.802     | 3.788     | **16.800%** | 🥉 3    | Low MAPE but higher error variance.                                  |

The **XGBRegressor** was selected as the final model because it provides the best balance between **accuracy (RMSE, MAE)** and **stability (MAPE)**.
After tuning (`subsample=0.6, n_estimators=500, max_depth=10, learning_rate=0.01`), performance consistently improved across all metrics.

---

#### **Feature Importance & Interpretation**

The most influential features for predicting delivery time are:

| Rank | Feature                     | Impact on Time | Interpretation                                                   |
| ---- | --------------------------- | -------------- | ---------------------------------------------------------------- |
| 1    | **Road Traffic Density**    | Positive       | Heavy traffic significantly increases delivery time.             |
| 2    | **Weather Conditions**      | Positive       | Adverse weather prolongs delivery time.                          |
| 3    | **Multiple Deliveries**     | Positive       | Multiple deliveries in a single trip cause delays.               |
| 4    | **Delivery Person Ratings** | Negative       | High-rated couriers tend to deliver faster and more efficiently. |

---

#### **Business Conclusion**

The **XGBRegressor** model with **MAPE 16.8%** provides highly accurate delivery time predictions.
Segment analysis shows the model performs best in the **High-Time Segment** (MAPE = 11.12%), demonstrating strong predictive capability for long-duration deliveries.

| Time Segment  | MAPE       | Interpretation                                   |
| ------------- | ---------- | ------------------------------------------------ |
| Low-Time      | 21.70%     | High variability for short deliveries.           |
| Medium-Time   | 17.58%     | Performance fairly stable.                       |
| **High-Time** | **11.12%** | Highly accurate predictions for long deliveries. |

Therefore, this model is **suitable for initial implementation** in a *delivery ETA prediction system*.
Companies can integrate it into operational dashboards to provide more realistic delivery time estimates for customers and logistics managers.

---

#### **Why Machine Learning?**

Machine learning provides significant advantages over traditional methods like historical averages or simple linear regression:

| Aspect              | Traditional Method                               | Machine Learning                                                     |
| ------------------- | ------------------------------------------------ | -------------------------------------------------------------------- |
| Data Complexity     | Only handles linear relationships                | Can learn non-linear feature interactions (e.g., traffic × weather). |
| Adaptability        | Difficult to adapt to changing conditions        | Can be updated regularly with new data.                              |
| Prediction Accuracy | General and non-specific predictions             | Can achieve low error (<17%) with tuning and spatial features.       |
| Business Impact     | Estimates often inaccurate → customer complaints | Accurate predictions → improved satisfaction and route efficiency.   |

In other words, machine learning can **convert operational data into precise business decisions**, resulting in cost efficiency, higher courier productivity, and improved customer satisfaction.

---

#### **Recommendations**

**A. Business Strategies**

1. **Delivery Route Optimization**
   Use predicted delivery times to determine the fastest routes based on real-time traffic and weather conditions.

2. **Resource Adjustment During Festival Periods**
   Increase courier numbers or delivery time allocation in Semi-Urban areas during high-demand periods.

3. **Courier Incentive System**
   Provide incentives to high-rated couriers as they significantly influence delivery efficiency.

4. **Enhanced Customer Transparency**
   Integrate the model into the app to show customers more accurate delivery time estimates.

**B. Technical Strategies**

1. **Integration of Geodesic Spatial Data**
   Use actual distances (haversine/geodesic) instead of city-level representation.

2. **Model Deployment via API / Dashboard**
   Implement XGBRegressor in the backend to allow automatic access to predictions by the application.

3. **Continuous Model Development**
   Retrain the model periodically (e.g., monthly) to maintain accuracy with the latest data.

4. **Experiment with Dynamic Features**
   Add features like *real-time traffic density*, *rainfall intensity*, or *delivery clustering by zone* to further improve model performance.

---

#### **Closing Note**

With a **MAPE of 16.8%**, the model demonstrates strong and stable predictive capability.
The machine learning regression approach has proven superior to conventional methods, providing **actionable insights** for operational and strategic decision-making in modern logistics.


