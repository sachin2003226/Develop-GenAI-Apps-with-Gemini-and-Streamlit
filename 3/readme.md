# Getting Started with the Gemini API in Vertex AI

# Vertex AI Workbench Lab: Using Gemini 2.0 Flash

This guide walks you through the process of using the **Gemini 2.0 Flash model** in Vertex AI Workbench.

---

## 🧪 Task 1: Open the Notebook in Vertex AI Workbench

1. Go to the **Google Cloud Console**.
2. From the **Navigation menu**, navigate to:
   - `Vertex AI > Workbench`
3. Find the instance named **instance** and click **Open JupyterLab**.
4. The JupyterLab interface will open in a new browser tab.

---

## ⚙️ Task 2: Set up the Notebook

1. Open the specified **notebook** file.
2. In the **Select Kernel** dialog, choose `Python 3`.
3. Run the following notebook sections:
   - `Getting Started`
   - `Import libraries`

4. Use:
   - **Project ID**: `Project ID`
   - **Location**: `Region`

> ⏱️ Note: Skip any cells labeled **Colab only**. If a cell throws a 429 error, wait a minute before retrying.

---

## 💬 Task 3: Use the Gemini 2.0 Flash Model

### ✅ Generate text from text prompts

- Use the `generate_content()` method to send a text prompt.
- Supports use cases like:
  - Multi-turn chat
  - Multimodal input

🔲 **Check my progress**: Generate text from text prompts

---

### 🔄 Streaming

- Stream responses from the model in real-time as they are being generated.

🔲 **Check my progress**: Streaming

---

### 🧪 Try your own prompts

- Customize your own prompts and run them through the model.

🔲 **Check my progress**: Try your own prompts

---

### 🔒 Safety Filters

- Use Gemini API's **safety filters** to control content categories.
- Analyze **safety ratings** in model responses.

🔲 **Check my progress**: Safety filters

---

### 💬 Test chat prompts

- Run multi-turn conversation examples using text prompts.

🔲 **Check my progress**: Test chat prompts

---

## 🖼️ Task 4: Generate Text from a Multimodal Prompt

### 🖼️ Generate text from local image and text

- Use a **local image file** and **text prompt** to generate a response.

🔲 **Check my progress**: Generate text from local image and text

---

### 🖼️ Generate text from text and image(s)

- Combine text and image(s) in a single prompt.

🔲 **Check my progress**: Generate text from text and image(s)

---

### 🖼️ Combining multiple images and text prompts for few-shot prompting

- Use **few-shot learning** technique with multiple image-text pairs.

🔲 **Check my progress**: Combining multiple images and text prompts for few-shot prompting

---

### 🎥 Generate text from a video file

- Upload a video and generate relevant textual responses.

🔲 **Check my progress**: Generate text from a video file

---

### 🌐 Direct analysis of publicly available web media

- Analyze media content directly from a public URL.

🔲 **Check my progress**: Direct analysis of publicly available web media

---


