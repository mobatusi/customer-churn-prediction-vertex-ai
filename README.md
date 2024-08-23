# customer-churn-prediction-vertex-ai
The project utilizes a customer dataset that includes spending data and churn labels to train an AutoML model, which is then deployed on Vertex AI for real-time churn prediction.


## Prerequisites

Before you begin, ensure you have the following:

- A Google Cloud project with billing enabled.
- Google Cloud SDK installed and authenticated.
- Python 3.7 or later installed.
- Required Python packages installed (listed in `requirements.txt`).

Also, be sure to enable the following APIs and services in your created project using the given commands provided along with the API in the terminal:

For Vertex AI API:
```sh
gcloud services enable vertexai.googleapis.com

For Cloud OS Login API:
gcloud services enable oslogin.googleapis.com

For Cloud Storage:
gcloud services enable storage.googleapis.com

For Compute Engine API:
gcloud services enable compute.googleapis.com
```

## Setup

1. **Clone the repository**:
   ```sh
   git clone https://github.com/mobatusi/customer-churn-prediction-vertex-ai.git
   cd customer-churn-prediction-vertex-ai
2. **Install the required packages**:

    ```
    pip install -r requirements.txt
    ```

3. **Set up your Google Cloud environment**:
    - Create a service account and download the JSON key file.

    - Set the environment variable for the service account:

    ```sh
    export GOOGLE_APPLICATION_CREDENTIALS="path/to/your-service-account-key.json"
    ```
4. Update the .env file:
    - Create a .env file in the root directory of the project and add the following environment variables:

    ```sh
    PROJECT_ID=your-google-cloud-project-id
    REGION=your-region
    BUCKET_URI=your-gcs-bucket-uri
    ```

## Using the Notebook
1. **Preprocess Data**
The notebook starts with data preprocessing. Ensure your dataset is available and update the notebook to point to your dataset location. The preprocessing steps include handling missing values, encoding categorical variables, and splitting the data into training and test sets.

2. **Train the Model**
Follow the steps in the notebook to train a machine learning model using your preprocessed data. The notebook uses Google Cloud AI Platform for training, so ensure your environment is correctly set up.

3. **Deploy the Model**
After training the model, the notebook guides you through deploying the model to an endpoint on Google Cloud AI Platform. The deployment steps include:

    - Creating a model resource.
    - Deploying the model to an endpoint.
4. **Make Online Predictions**
Once the model is deployed, you can use the endpoint to make online predictions. The notebook includes code to prepare the endpoint and make predictions using the deployed model.

Here is an example snippet from the notebook to check the deployed models and make predictions:

```python
    # Prepare the endpoint even after the session timeout
    endpoint = aiplatform.Endpoint(endpoint_name='123456')
    deployed_models = endpoint.list_models()
    if not deployed_models:
        print("no models deployed yet")
    else:
        for deployed_model in deployed_models:
            if deployed_model.display_name == "adopted-prediction-model":
                print("Model deployed, you can move to prediction phase")

    # Example code to make a prediction
    prediction = endpoint.predict(instances=[your_instance_data])
    print("Prediction:", prediction)
```    

## Conclusion
By following the steps in the notebook, you can develop a customer churn prediction model, deploy it to Google Cloud AI Platform, and make online predictions. Ensure you have the necessary permissions and configurations set up in your Google Cloud project.