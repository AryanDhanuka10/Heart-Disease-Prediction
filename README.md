# Heart Failure Prediction System

## Overview
This project implements a dual-model approach for heart failure prediction using both clinical data and MRI images. The system combines a Random Forest model for analyzing clinical parameters and a Convolutional Neural Network (CNN) for processing medical imaging data, providing medical professionals with comprehensive diagnostic support.

![heartimage](https://media.gettyimages.com/id/1320270583/photo/close-up-of-man-is-heart-attack.jpg?s=2048x2048&w=gi&k=20&c=qM8XA9gSBeqvJXqB0hXbP06XwoYApHJoEw_lDt-1LjQ=)

[Visit Deployed App](https://heart-failure-prediction-aryandhanuka10.streamlit.app/)

## Features
- **Dual Prediction Methods**:
  - Clinical data analysis using Random Forest
  - MRI image analysis using CNN
- **Interactive Web Interface**:
  - User-friendly Streamlit application
  - Real-time predictions

## Project Structure
```
heart_failure_pred/
├── artifacts/
│   ├── data/
│   │   ├── img_data/
│   │   │   ├── normal/
│   │   │   └── failure/
│   │   └── tabular_data/
│   │       └── heart_failure.csv
│   └── models/
│       ├── cnn/
│       │   ├── cnn_model.keras
│       │   └── cnn_score.json
│       └── rf/
│           ├── rf_model.pkl
│           └── rf_score.json
├── main.py
├── utils.py
├── app.py
├── requirements.txt
└── README.md
```

## Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Setup
1. Clone the repository:
```bash
git clone https://github.com/AryanDhanuka10/Heart-Failure-Prediction.git
cd heart_failure_pred
```

2. Create and activate a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows, use: venv\Scripts\activate
```

3. Install required packages:
```bash
pip install -r requirements.txt
```

## Model Training

### Train Models
To train both the Random Forest and CNN models:
```bash
python main.py
```

This script will:
- Load and preprocess the data
- Train the Random Forest model with hyperparameter tuning
- Train the CNN model
- Save the trained models and their performance metrics

## Using the Web Interface

### Start the Application
```bash
streamlit run app.py
```

### Making Predictions

#### Clinical Data Prediction
1. Navigate to the "Clinical Data Prediction" tab
2. Enter the required clinical parameters:
   - Age
   - Anaemia status
   - Creatinine phosphokinase level
   - Diabetes status
   - Ejection fraction
   - High blood pressure status
   - Platelets count
   - Serum creatinine level
   - Serum sodium level
   - Sex
   - Smoking status
   - Follow-up period
3. Click "Predict" to get results

#### MRI Image Prediction
1. Navigate to the "MRI Image Prediction" tab
2. Upload a DICOM format MRI image
3. View the prediction results

## Technical Details

### Data Format Requirements

#### Clinical Data
- All numerical inputs should be non-negative
- Binary inputs (anaemia, diabetes, high blood pressure, sex, smoking) use 0/1 encoding
- Input ranges:
  - Age: 0-100 years
  - Ejection Fraction: 0-100%
  - Platelets: typical range 150,000-450,000 per μL
  - Time: measured in days

#### Image Data
- Format: DICOM (.dcm)
- Processed to 224x224 pixels
- Normalized to [0,1] range

### Models

#### Random Forest Model
- Features: 12 clinical parameters
- Hyperparameter tuning via GridSearchCV
- Optimization metric: Accuracy
- Output: Binary classification with probability scores

#### CNN Model
- Architecture: Sequential model with multiple convolutional layers
- Input shape: (224, 224, 1)
- Training: Adam optimizer with sparse categorical crossentropy
- Output: Binary classification (normal/failure)

## Performance Metrics
The system saves performance metrics for both models:
- For Random Forest: accuracy, F1 score, and detailed classification report
- For CNN: loss and accuracy metrics

## Contributing
Please read CONTRIBUTING.md for details on our code of conduct and the process for submitting pull requests.

## Acknowledgments
- Dataset sources
   - https://www.cardiacatlas.org/sunnybrook-cardiac-data/
   - https://www.kaggle.com/datasets/andrewmvd/heart-failure-clinical-data
