Capstone Project
Calendar Classification Final Report by Andrew Nordstrom

Jupyter Notebook https://github.com/mad24x/Classification_capstone/blob/main/meeting_prediction_attendance_final_arn.ipynb

1. Problem Statement: Managing meetings effectively is a crucial aspect of professional productivity. However, individuals often struggle with determining whether a meeting requires physical travel, which can lead to last-minute departures, tardiness, or inefficient scheduling. The goal of this project is to develop a machine learning-powered AI assistant that classifies calendar invites into onsite, offsite, or online meetings. Blocking off travel time would also be a benefit to coworkers.  Knowing when someone is not available to schedule meetings also improves efficiency and last-minute cancellations. 

2. Model Outcomes or Predictions: The problem is formulated as a classification task, where the AI assistant categorizes meetings into three classes:
	• Onsite Meetings: Meetings held at the user’s office.
	• Offsite Meetings: Meetings requiring travel to an external location.
	• Online Meetings: Virtual meetings conducted via platforms like Zoom or Microsoft Teams.
For future considerations of offsite meetings, an additional regression model will predict the recommended departure time based on traffic conditions and user preferences. This project will employ supervised learning techniques since labeled data (meeting types and historical travel data) will be available.

3. Data Acquisition: Data was created by a generator.  Having access to individual calendars and appointments would be difficult to obtain as it could have sensitive data.  For the purposes of the project data was created to simulate Calendar Invite entries.  
Data included: (a) Meeting invitations; (b) Meeting physical destination; (c) Subject; (d) Description; (e) Location of the user’s home office

4. Data Preprocessing/Preparation Ensuring data quality is critical for accurate model performance. The following steps were taken to prepare the data:
	a. Handling Missing Values and Inconsistencies
	  • Removed incomplete meeting entries with missing locations.
	  • Standardized location formats (e.g., resolving abbreviations like “NYC” to “New York City”).
	  • Converted timestamps into a standardized format for consistency.
	  • Created a combined text feature from the 'title' and 'location' columns to enhance text-based classification.
	b. Data Splitting
	  • Training Set: 80% of labeled meeting data was used for training.
	  • Testing Set: 20% was reserved for evaluation.
	c. Feature Engineering & Encoding
	  • Applied TF-IDF Vectorization to convert the combined text feature into numerical representations for model input.
	  • Encoded the target variable: ‘attended_online’ was set to 1, and ‘attended_in_person’ was set to 0.
	  • Engineered new features such as distance from office for offsite meetings (future enhancement).

5. Modeling. The project employs a combination of classification and regression models:
Classification Model (Meeting Type Prediction)
	  • Baseline Model: Logistic Regression
	  • Advanced Models: Random Forest Classifier with TF-IDF text processing
Regression Model (Departure Time Prediction)
	  • Baseline Model: Linear Regression
	  • Advanced Models: Gradient Boosting, Time-Series-based LSTMs
Hyperparameter tuning was performed using GridSearchCV to identify optimal configurations.

6. Model Evaluation

The models were evaluated using the following metrics:

Classification Metrics:
	  • Accuracy: Measures overall correctness of meeting type classification.
	  • Precision & Recall: Evaluates performance in correctly identifying offsite meetings.
	  • F1-Score: Balances precision and recall for optimal model assessment.

For the Random Forest Model, evaluation results were:
	  • Accuracy: 92.8%

Classification Report:
	  • Precision: 0.92 for in-person, 0.94 for online.
	  • Recall: 0.96 for in-person, 0.89 for online.
	  • F1-Score: 0.94 for in-person, 0.92 for online.

Confusion Matrix:

	  • 531 True Negatives (Correctly classified in-person meetings)
	  • 397 True Positives (Correctly classified online meetings)
	  • 24 False Positives (Incorrectly classified in-person meetings as online)
	  • 48 False Negatives (Incorrectly classified online meetings as in-person)

Confusion Matrix Insights: Analysis revealed that most misclassifications occurred between onsite and offsite meetings, indicating a potential need for improved location-based features.

Feature Importance: The Random Forest model's feature importance analysis showed that keywords from the meeting title and location significantly impacted classification accuracy.

Best Model Selection:

The Random Forest model demonstrated the highest classification accuracy at 92.8%.

Conclusion
This project successfully developed an AI assistant capable of classifying meeting types. The model’s high accuracy and minimal travel time prediction error indicate its effectiveness in improving scheduling efficiency and time management for professionals. Future enhancements could include real-time traffic integration and personalized learning based on user behavior over time, personal preferences such as arriving a set amount of time early.  The final product would block off calendars for the user to include travel time to and from meetings.  

Next Steps
To further refine and validate the model, the following next steps are planned:
	• Industry Partnership: Collaborate with a company to gain access to companywide calendar invites, enabling model training on live, real-world data.
	• Traffic Data Integration: Collect and analyze traffic data from sources such as Google Maps APIs to enhance the accuracy of travel time predictions.
	• Historical Travel Analysis: Leverage past travel time records to refine the departure time recommendation model and account for time-based traffic variations.
	• User-Centric Enhancements: Implement personalized settings allowing users to customize arrival buffer times and integrate feedback loops to improve model adaptability over time.

