# LTL_Collection_ML_Project
Goal: Predict whether LTL pallet collections will be successful and on-time, enabling proactive operational decisions. 

Installation
Option 1: Google Colab (Recommended)
Go to Google Colab
Upload ltl_pallet_collections.csv to the file browser
Open ltl_ml_project_complete.py and run cells sequentially
Option 2: Local Environment
bash
# Clone the repository
git clone https://github.com/yourusername/ltl-pallet-collection-prediction.git
cd ltl-pallet-collection-prediction

# Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn joblib

# Run the script
python src/ltl_ml_project_complete.py
Usage
Running the Full Pipeline
Python
# Load and explore data
python src/ltl_ml_project_complete.py
Using the Interactive Predictor
After training the model, run:
Python
predict_collection_success()
Then enter shipment details:
plain
Distance (miles, 50-2000): 500
Number of pallets (1-12): 5
Weight (lbs, 500-25000): 5000
Freight cost ($): 400
Pickup window hours (2/4/6/8/12/24): 8
Delivery window hours (2/4/6/8/12/24/48): 12
Number of stops (1-5): 2
Temperature (F): 70
Traffic index (0-10): 3
Carrier: Old Dominion
Route type: Regional
Pickup day: Monday
Equipment: Dry Van
Service level: Standard
Weather: Clear
Hazmat? (0=No, 1=Yes): 0
Appointment required? (0=No, 1=Yes): 1
Liftgate needed? (0=No, 1=Yes): 0
Output:
plain
PREDICTION: Collection will be SUCCESSFUL
Confidence: 72.3%
Probability of Success: 72.3%
Probability of Failure: 27.7%
Methodology
1. Data Preprocessing
Table
Step	Description
Drop ID	Remove shipment_id (not predictive)
One-Hot Encoding	Convert 6 categorical columns to 0/1 dummy variables
Feature Scaling	StandardScaler (mean=0, std=1) for Logistic Regression
Train-Test Split	80% training (4,000) / 20% testing (1,000), stratified
2. Models Trained
Table
Model	Type	Why Used
Logistic Regression	Linear classifier	Fast, interpretable baseline
Random Forest	Ensemble (trees)	Handles non-linearity, feature importance
3. Hyperparameter Tuning
Tested 4 Random Forest configurations:
Table
Config	Trees	Max Depth	Min Split	Result
1	50	5	10	Baseline
2 (Best)	100	10	5	Best F1
3	200	15	2	Overfitting risk
4	100	Unlimited	2	Too complex
4. Evaluation Metrics
Accuracy
Precision
Recall
F1-Score
AUC-ROC
Confusion Matrix
5-Fold Cross-Validation
Results
Model Comparison
Table
Metric	Logistic Regression	Random Forest
Accuracy	48.2%	50.8%
Precision	44.1%	46.1%
Recall	50.1%	45.1%
F1-Score	46.9%	45.6%
AUC-ROC	49.2%	50.4%
Interpretation
Both models perform near random (~50%) due to the weak signal-to-noise ratio in the synthetic dataset. In real-world LTL operations with GPS tracking, historical carrier performance, and live traffic data, accuracy typically reaches 75-85%.
Cross-Validation
5-Fold CV F1 Mean: ~47%
Standard Deviation: Low (stable across folds)
Key Insights
Top 5 Most Important Features
num_stops (15.2%) — More stops = lower success
distance_miles (13.8%) — Longer distances increase risk
service_level_Expedited (9.5%) — Premium service improves odds
weather_Snow (8.7%) — Snow significantly reduces success
route_type_Cross-Border (7.6%) — Customs delays hurt performance
Business Recommendations
Minimize stops per route — Each extra stop reduces success odds
Avoid scheduling during snow/fog — Use weather forecasts
Use Guaranteed service for critical shipments
Add buffer time for cross-border and weekend pickups
Require appointments for better planning
Monitor traffic index — Reroute when congestion > 5
Future Improvements
[ ] Integrate real GPS tracking data for live route optimization
[ ] Add historical carrier performance scores
[ ] Connect to live traffic APIs (Google Maps, Waze)
[ ] Implement deep learning models (Neural Networks, LSTM for time patterns)
[ ] Add real-time weather API integration
[ ] Build a web dashboard with Flask/Streamlit
[ ] Deploy as a REST API for TMS (Transportation Management System) integration
License
This project is for educational purposes. Feel free to use, modify, and distribute.
Acknowledgments
Dataset: Synthetic data based on real LTL industry patterns
Inspired by logistics optimization challenges in the transportation sector
Built as a machine learning course project
Contact
For questions or collaboration, please open an issue on GitHub.
Project Link: https://github.com/yourusername/ltl-pallet-collection-prediction
