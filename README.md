# Swiggy Food Delivery Time Prediction App

This repository contains a FastAPI application for predicting food delivery times based on various features such as delivery person information, weather conditions, traffic, and other relevant factors. The application uses a pre-trained machine learning model registered in MLflow and a preprocessing pipeline.

## Features
- **FastAPI Framework**: Provides RESTful API endpoints for interaction.
- **MLflow Integration**: Uses MLflow for model management and tracking.
- **DagsHub Integration**: Tracks and retrieves model details from DagsHub.
- **Preprocessing Pipeline**: Data cleaning and preprocessing steps included.
- **Prediction Endpoint**: Allows users to input data and get predictions.

---

## Project Structure
```plaintext
.
├── app.py                  # Main FastAPI application code
├── run_information.json    # JSON file containing model metadata
├── models/
│   └── preprocessor.joblib # Preprocessing pipeline file
├── scripts/
│   └── data_clean_utils.py # Utility functions for data cleaning
├── requirements.txt        # Python dependencies
└── README.md               # Project documentation
```

---

## Getting Started

### Prerequisites
1. Python 3.8 or higher
2. Dependencies listed in `requirements.txt`
3. Access to DagsHub repository for MLflow tracking

### Installation

1. Clone this repository:
    ```bash
    git clone https://github.com/<your_username>/swiggy-delivery-time-prediction.git
    cd swiggy-delivery-time-prediction
    ```

2. Create and activate a virtual environment:
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3. Install the required dependencies:
    ```bash
    pip install -r requirements.txt
    ```

4. Set up the MLflow tracking URI (update in `app.py` if needed):
    ```python
    mlflow.set_tracking_uri("https://dagshub.com/<repo_owner>/<repo_name>.mlflow")
    ```

---

## Usage

1. Start the FastAPI application:
    ```bash
    uvicorn app:app --host 0.0.0.0 --port 8000
    ```

2. Navigate to the API documentation:
    - Open your browser and visit: `http://localhost:8000/docs`
    
3. Make predictions using the `/predict` endpoint:
    - Provide input data in the required JSON format.
    - Receive the predicted delivery time as the response.

---

## Input Data Format
The `/predict` endpoint expects input in the following JSON format:
```json
{
  "ID": "12345",
  "Delivery_person_ID": "DP001",
  "Delivery_person_Age": "30",
  "Delivery_person_Ratings": "4.5",
  "Restaurant_latitude": 19.0760,
  "Restaurant_longitude": 72.8777,
  "Delivery_location_latitude": 19.2183,
  "Delivery_location_longitude": 72.9781,
  "Order_Date": "2025-01-25",
  "Time_Orderd": "18:30:00",
  "Time_Order_picked": "18:45:00",
  "Weatherconditions": "Sunny",
  "Road_traffic_density": "High",
  "Vehicle_condition": 5,
  "Type_of_order": "Veg",
  "Type_of_vehicle": "Bike",
  "multiple_deliveries": "1",
  "Festival": "No",
  "City": "Mumbai"
}
```

---

## Key Components

### 1. **Data Preprocessing**
Data is cleaned and transformed using a preprocessing pipeline stored in `models/preprocessor.joblib`.

### 2. **Model Retrieval**
The application retrieves the latest production-ready model using MLflow and DagsHub integration.

### 3. **Endpoints**
- **Home Endpoint (`/`)**: Returns a welcome message.
- **Predict Endpoint (`/predict`)**: Accepts input data and returns delivery time predictions.

---

## Configuration
### DagsHub Integration
- Initialize DagsHub in `app.py`:
    ```python
    dagshub.init(repo_owner='msa23003',
                 repo_name='swiggy-delivery-time-prediction',
                 mlflow=True)
    ```

### MLflow Configuration
- Set the MLflow tracking URI:
    ```python
    mlflow.set_tracking_uri("https://dagshub.com/<repo_owner>/<repo_name>.mlflow")
    ```

---

## Deployment
This application can be deployed using any cloud platform or containerized using Docker.

### Example Dockerfile
```dockerfile
FROM python:3.8-slim

WORKDIR /app

COPY . /app

RUN pip install -r requirements.txt

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```

---

## License
This project is licensed under the MIT License. See the LICENSE file for details.

---

## Acknowledgments
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [MLflow Documentation](https://www.mlflow.org/docs/latest/index.html)
- [DagsHub Documentation](https://dagshub.com/docs/)

Feel free to fork and contribute to this repository!
