# anomaly_XGBoostOil Production Anomaly Detection Using XGBoost
Project Overview
This project focuses on detecting unusual changes in daily oil production for well A01 using machine learning.
The main idea is to predict expected oil production based on previous-day production, reservoir pressure, and water cut. Actual production is then compared with predicted production to identify observations with unusually large deviations.
Dataset
The analysis uses the following variables:
• date: Observation date
• well_id: Well identifier
• actual_oil_bopd: Actual oil production rate in barrels of oil per day
• pressure_psi: Reservoir pressure in psi
• water_cut_pct: Water cut percentage
Methodology
1. Data Preparation
The data was filtered to include well A01 and sorted by date. Lagged features were created using the previous row’s values. Rows with missing values in the required features were removed.
2. Feature Engineering
The following features were used as model inputs:
• Previous-day oil production
• Previous-day reservoir pressure
• Previous-day water cut
The target variable was actual daily oil production.
3. Production Prediction with XGBoost
An XGBoost regression model was used to predict oil production.
The model was trained using the first 365 observations. After that, a walk-forward prediction approach was applied: the model was repeatedly trained on available historical data to predict the next observation.
4. Residual Analysis
Prediction errors were calculated by subtracting predicted production from actual production.
Error = Actual Production - Predicted Production
These errors were used to measure how much actual production deviated from the model’s expectations.
5. Anomaly Detection
The first 180 out-of-sample prediction errors were used to calculate a baseline and detection threshold.
The median and Median Absolute Deviation (MAD) were used to establish a robust threshold. Observations in the subsequent test period were flagged as anomalies when their errors deviated from the baseline by more than the threshold.
6. Visualization
Actual and predicted oil production were plotted over time. Detected anomalies were highlighted on the chart to make unusual production behavior easier to identify.
Tools and Libraries
• Python
• Pandas
• XGBoost
• Matplotlib
Conclusion
This project demonstrates a straightforward approach to detecting potential oil production anomalies using machine learning and statistical residual analysis.
By comparing actual production with expected production, the method identifies dates that may require further investigation. Petroleum engineering knowledge can then help interpret these unusual patterns alongside reservoir pressure, water cut, and other available operational information.
Limitations
The current implementation analyzes one well, A01. Anomalies indicate unusual deviations from model predictions and do not necessarily confirm equipment failure or a specific reservoir issue. Further investigation is required to determine the cause of each flagged observation.
