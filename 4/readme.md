
---

# 🚀 Task 1: Build and Deploy the Application to Cloud Run

In this section, you will deploy the **Streamlit Application** on **Cloud Run**.

---

## 🧩 Step 1: Clone the Repository

1. Open a new **Cloud Shell** terminal by clicking on the **Cloud Shell icon** in the top-right corner of the Cloud Console.
2. Run the following commands:

```bash
git clone https://github.com/GoogleCloudPlatform/generative-ai.git --depth=1
cd generative-ai/gemini/sample-apps/gemini-streamlit-cloudrun
```

---

## ⚙️ Step 2: Configuration

### Set up Python Virtual Environment & Install Dependencies:

```bash
python3 -m venv gemini-streamlit
source gemini-streamlit/bin/activate
pip install -r requirements.txt
```

---

## 🌍 Step 3: Set Environment Variables

Your application needs access to two environment variables:

- `GOOGLE_CLOUD_PROJECT` – Your Google Cloud Project ID  
- `GOOGLE_CLOUD_REGION` – The deployment region (e.g., `us-central1`)

Set them with:

```bash
GOOGLE_CLOUD_PROJECT='qwiklabs-gcp-02-5ba98718a9a5'
GOOGLE_CLOUD_REGION='europe-west4'
```

These are required by this line in the `app.py`:

```python
vertexai.init(project=PROJECT_ID, location=LOCATION)
```

---

## 📦 Step 4: Build Docker Image & Push to Artifact Registry

Set required environment variables and create the Artifact Registry:

```bash
AR_REPO='gemini-repo'
SERVICE_NAME='gemini-streamlit-app'

gcloud artifacts repositories create "$AR_REPO" \
  --location="$GOOGLE_CLOUD_REGION" \
  --repository-format=Docker
```

Now build and submit the Docker image:

```bash
gcloud builds submit --tag "$GOOGLE_CLOUD_REGION-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/$AR_REPO/$SERVICE_NAME"
```

> 🕒 This step may take a few minutes.

✅ **Output Sample:**
```
DONE
--------------------------------------------------------------------------------
ID                                    CREATE_TIME                DURATION  SOURCE
a601ffd1-c282-43d2-942c-53cc13f43bf2  2023-12-18T11:37:30+00:00  2M29S     ...
IMAGES: europe-west4-docker.pkg.dev/qwiklabs-gcp-02.../gemini-repo/gemini-streamlit-app
STATUS: SUCCESS
```

---

## 🚀 Step 5: Deploy to Cloud Run

Use the image you pushed to deploy the service:

```bash
gcloud run deploy "$SERVICE_NAME" \
  --port=8080 \
  --image="$GOOGLE_CLOUD_REGION-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/$AR_REPO/$SERVICE_NAME" \
  --allow-unauthenticated \
  --region=$GOOGLE_CLOUD_REGION \
  --platform=managed  \
  --project=$GOOGLE_CLOUD_PROJECT \
  --set-env-vars=GOOGLE_CLOUD_PROJECT=$GOOGLE_CLOUD_PROJECT,GOOGLE_CLOUD_REGION=$GOOGLE_CLOUD_REGION
```

✅ **Successful Output:**
```
✓ Deploying new service... Done.

Done.
Service [gemini-streamlit-app] revision [gemini-streamlit-app-00001-srg] has been deployed and is serving 100 percent of traffic.

Service URL: https://gemini-streamlit-app-hc2gb6hsia-uc.a.run.app
```

---

## 🧠 Step 6: Interact with Vertex Gemini

Visit the **Service URL** in your browser.

Choose a functionality in the app – it will use the **Gemini API** via **Vertex AI** to generate responses!

---


