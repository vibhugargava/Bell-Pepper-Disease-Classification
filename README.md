# Bell Pepper Disease Identification
This is a Deep Learning Project in the agricultural domain. Image Classification is done using Convolutional Neural Network. For training, I have taken the data of Bell Pepper from the "PlantVillage" dataset. (https://www.kaggle.com/datasets/arjuntejaswi/plant-village)
The technology Stack for this project is:-
1. Model Building: tensorflow, CNN, data augmentation
2. Backend Server: FastAPI
3. Model Optimization: Quantization
4. Frontend: React JS
5. Deployment: GCP (Google cloud platform, GCF (Google cloud functions)

The model is deployed to GCP so that the model can be accessed using a mobile app (In Progress).

## Setup for Python:

1. Install Python ([Setup instructions](https://wiki.python.org/moin/BeginnersGuide))

2. Install Python packages

```
pip3 install -r training/requirements.txt
pip3 install -r api/requirements.txt
```
## Setup for ReactJS

1. Install Nodejs ([Setup instructions](https://nodejs.org/en/download/package-manager/))
2. Install NPM ([Setup instructions](https://www.npmjs.com/get-npm))
3. Install dependencies

```bash
cd frontend
npm install --from-lock-json
npm audit fix
```

4. Copy `.env.example` as `.env`.

5. Change API url in `.env`.
  - 2.1 Only for mac users
```bash
cd ios && pod install && cd ../
```

3. Copy `.env.example` as `.env`.

4. Change API url in `.env`.

## Training the Model

1. Download the data from [kaggle](https://www.kaggle.com/arjuntejaswi/plant-village).
2. Only keep folders related to Potatoes.
3. Run Jupyter Notebook in Browser.

```bash
jupyter notebook
```

4. Open `training/potato-disease-training.ipynb` in Jupyter Notebook.
5. In cell #2, update the path to dataset.
6. Run all the Cells one by one.
7. Copy the model generated and save it with the version number in the `models` folder.

## Running the API

### Using FastAPI

1. Get inside `api` folder

```bash
cd api
```

2. Run the FastAPI Server using uvicorn

```bash
uvicorn main:app --reload --host 0.0.0.0
```

3. Your API is now running at `0.0.0.0:8000`
## Running the Frontend

1. Get inside `api` folder

```bash
cd frontend
```

2. Copy the `.env.example` as `.env` and update `REACT_APP_API_URL` to API URL if needed.
3. Run the frontend

```bash
npm run start
```
## Deploying the TF Model (.h5) on GCP

1. Create a [GCP account](https://console.cloud.google.com/freetrial/signup/tos?_ga=).
2. Create a [Project on GCP](https://cloud.google.com/appengine/docs/standard/nodejs/building-app/creating-project) (Keep note of the project id).
3. Create a [GCP bucket](https://console.cloud.google.com/storage/browser/).
4. Upload the tf .h5 model generate in the bucket in the path `models/potato-model.h5`.
5. Install Google Cloud SDK ([Setup instructions](https://cloud.google.com/sdk/docs/quickstarts)).
6. Authenticate with Google Cloud SDK.

```bash
gcloud auth login
```

7. Run the deployment script.

```bash
cd gcp
gcloud functions deploy predict --runtime python38 --trigger-http --memory 512 --project project_id
```

8. Your model is now deployed.
9. Use Postman to test the GCF using the [Trigger URL](https://cloud.google.com/functions/docs/calling/http).
