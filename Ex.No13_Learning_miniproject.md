# Ex.No: 10 Learning – Use Supervised Learning  
### DATE: 12/05/2025                                                                           
### REGISTER NUMBER : 212222060182
### AIM: 
  To develop a machine learning model using the Random Forest Classifier to accurately detect the presence of eyes in image data by processing and classifying features from an ARFF dataset.


###  Algorithm:

1.Import necessary modules: pandas, numpy, sklearn, arff, etc.

2.Mount Google Drive using drive.mount()

3.Load the .arff dataset using the liac-arff package.

4.Convert the data into a Pandas DataFrame.

5.Separate features (X) and target labels (y) from the DataFrame.

6.Convert target labels to integer type if necessary.

7.Use train_test_split() to divide the data into training and testing sets (e.g., 80%-20%).

8.Standardize the feature values using StandardScaler to bring them to a common scale.

9.Initialize a RandomForestClassifier with parameters like n_estimators=100.

10.Fit the model on the training data.

11.Predict the output for the test set using the trained model.

12.Use accuracy_score, confusion_matrix, and classification_report to evaluate the model's performance.

### Program:

  import pandas as pd
  import numpy as np
  from sklearn.model_selection import train_test_split
  from sklearn.preprocessing import StandardScaler
  from sklearn.ensemble import RandomForestClassifier
  from sklearn.metrics import classification_report, confusion_matrix, accuracy_score
  from google.colab import drive
  drive.mount('/content/drive')

  data_path = '/content/drive/My Drive/data.arff'  # Adjust to your file location
  !pip install liac-arff
  import arff
  with open(data_path, 'r') as f:
      dataset = arff.load(f)
  [df = pd.DataFrame(dataset['data'], columns=[attr[0] for attr in dataset['attributes']])

  X = df.drop('eyeDetection', axis=1)
  y = df['eyeDetection'].astype(int)

  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

  scaler = StandardScaler()
  X_train_scaled = scaler.fit_transform(X_train)
  X_test_scaled = scaler.transform(X_test)

  clf = RandomForestClassifier(n_estimators=100, random_state=42)
  clf.fit(X_train_scaled, y_train)

  y_pred = clf.predict(X_test_scaled)
  df.head()
  print(df.columns)
  print("Accuracy:", accuracy_score(y_test, y_pred))
  print("Confusion Matrix:\n", confusion_matrix(y_test, y_pred))
  print("Classification Report:\n", classification_report(y_test, y_pred)) 

### Output:

![WhatsApp Image 2025-05-19 at 20 50 43_938296c3](https://github.com/user-attachments/assets/601075f4-2ca6-4804-a96a-1ca002a9b5cc)
![WhatsApp Image 2025-05-19 at 20 50 43_7772a1d7](https://github.com/user-attachments/assets/e50d238e-ea25-4c28-851d-1d98d8f17192)

### Result:
Thus the system was trained successfully and the prediction was carried out.
