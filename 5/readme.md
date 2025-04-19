# Develop GenAI Apps with Gemini and Streamlit: Challenge Lab

## ✅ Task 1: Use cURL to test a prompt with the API

### Steps:
1. **Open Vertex AI > Workbench** from the Google Cloud Console.
2. Click **"Open JupyterLab"** for the instance shown.
3. Inside `prompt.ipynb`:
   - **In cell 3**, replace `PROJECT_ID` and `REGION` with the ones provided on the lab page.
   - **In cell 5**, replace the existing prompt with:

   ```bash
   I am a Chef.  I need to create Japanese recipes for customers who want low sodium meals. However, I do not want to include recipes that use ingredients associated with a peanuts food allergy. I have ahi tuna, fresh ginger, and edamame in my kitchen and other ingredients. The customer wine preference is red. Please provide some for meal recommendations. For each recommendation include preparation instructions, time to prepare and the recipe title at the beginning of the response. Then include the wine paring for each recommendation. At the end of the recommendation provide the calories associated with the meal and the nutritional facts.
   ```

4. **Run all cells** in the notebook.
5. **Save the notebook**.
6. Click **Check my progress** ✅.

---

## ✅ Task 2: Complete `chef.py` with Streamlit and Gemini prompt

### Steps:
1. In **Cloud Shell**, run:
   ```bash
   git clone https://github.com/GoogleCloudPlatform/generative-ai.git
   cd generative-ai/gemini/sample-apps/gemini-streamlit-cloudrun
   ```
2. Add dependencies to `requirements.txt`:
   ```
   google-cloud-logging
   google-cloud-aiplatform
   ```

3. Download `chef.py`:
   ```bash
   gsutil cp gs://spls/gsp517/chef.py .
   ```

4. Open `chef.py` in Cloud Shell Editor and do the following:
   - Add Streamlit radio button under existing input components:
     ```python
     wine = st.radio("Wine Preference", ["Red", "White", "None"])
     ```

   - Replace the existing prompt block with the updated one:
     ```python
     prompt = f"""I am a Chef.  I need to create {cuisine} \n
     recipes for customers who want {dietary_preference} meals. \n
     However, don't include recipes that use ingredients with the customer's {allergy} allergy. \n
     I have {ingredient_1}, \n
     {ingredient_2}, \n
     and {ingredient_3} \n
     in my kitchen and other ingredients. \n
     The customer's wine preference is {wine} \n
     Please provide some for meal recommendations.
     For each recommendation include preparation instructions,
     time to prepare
     and the recipe title at the beginning of the response.
     Then include the wine paring for each recommendation.
     At the end of the recommendation provide the calories associated with the meal
     and the nutritional facts.
     """
     ```

5. **Save the file**, then upload the modified `chef.py`:
   ```bash
   gcloud storage cp chef.py gs://[bucket-name-from-lab-instructions]/
   ```

> Replace `[bucket-name-from-lab-instructions]` with the correct bucket provided during lab start.

6. Click **Check my progress** ✅.

---

## ✅ Task 3: Test the application

1. Make sure you're still in:
   ```bash
   cd generative-ai/gemini/sample-apps/gemini-streamlit-cloudrun
   ```

2. Set up Python environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

3. Set your project and region:
   ```bash
   export PROJECT=$(gcloud config get-value project)
   export REGION=us-central1  # or your lab-provided region
   ```

4. Run the app:
   ```bash
   streamlit run chef.py
   ```

5. Test the app in the provided link.
6. Click **Check my progress** ✅.

---

## ✅ Task 4: Modify Dockerfile and push to Artifact Registry

### Steps:
1. Edit the `Dockerfile`:
   - Ensure it refers to `chef.py`, not any other sample file.

   Example:
   ```dockerfile
   COPY chef.py /app/chef.py
   CMD ["streamlit", "run", "/app/chef.py"]
   ```

2. Set environment variables:
   ```bash
   export AR_REPO=chef-repo
   export SERVICE_NAME=chef-streamlit-app
   ```

3. Create Artifact Registry and push image (run together):
   ```bash
   gcloud artifacts repositories create $AR_REPO \
     --repository-format=docker \
     --location=$REGION

   gcloud builds submit \
     --tag "$REGION-docker.pkg.dev/$PROJECT/$AR_REPO/$SERVICE_NAME"
   ```

4. Wait for the build to complete.
5. Click **Check my progress** ✅.

---

## ✅ Task 5: Deploy to Cloud Run and test

### Steps:
```bash
gcloud run deploy $SERVICE_NAME \
  --image="$REGION-docker.pkg.dev/$PROJECT/$AR_REPO/$SERVICE_NAME" \
  --platform=managed \
  --region=$REGION \
  --allow-unauthenticated \
  --port=8080 \
  --set-env-vars=PROJECT=$PROJECT,REGION=$REGION
```

- Wait for the service URL.
- Visit the URL and confirm the app works as expected.

