# Task 2 - Run instructions

This repository contains instructions to run the existing notebook that retrieves the last 10 additions from the target registry via the SODA API and saves a full snapshot of the dataset to disk.

## Open Task2.ipynb in Colab (one-click)

Run in the browser, no local setup required.

Open the notebook directly in Google Colab (this link opens the notebook from this repository and commit):

[Open Task2.ipynb in Colab](https://colab.research.google.com/github/CargoCultScientist/ny-opendata/blob/93c2d69e8453c19756dcb8a4229acb5e5c9d34e0/Task2.ipynb)

## Get the API keys from the source

This dataset is hosted on a Socrata Open Data portal. The notebook authenticates with the SODA API using an Application Key ID and Application Key Secret (basic-auth style credentials).

1. Sign in to the portal that hosts the dataset.
2. Go to your account or developer settings and create an Application Key. Socrata returns **two separate values**: an **App Token (Key ID)** and a **Secret**.
3. Copy both values. In this project, we store them as `NY_API_KEY_ID` and `NY_API_KEY_SECRET` to match the notebook’s variable names.

Reference: [Socrata Application Tokens](https://dev.socrata.com/docs/app-tokens.html)

## Insert the tokens in Colab

Choose one method.

### Method A - Colab Secrets panel

1. In Colab, open the left sidebar and click the key icon labeled "Secrets".  
2. Add secrets named **NY_API_KEY_ID** and **NY_API_KEY_SECRET** with your key ID and secret value. Enable Notebook access for the current notebook.
3. The notebook will load them via `google.colab.userdata.get`.

### Method B - Secure prompt inside the notebook

Insert a new cell:

```python
import os, getpass
os.environ["NY_API_KEY_ID"] = getpass.getpass("Paste your Application Key ID: ")
os.environ["NY_API_KEY_SECRET"] = getpass.getpass("Paste your Application Key Secret: ")
```

Then run the remaining cells.

> **Tip:** If you prefer not to modify the notebook, you can also open the “Runtime ▶ Run all…” menu after setting the secrets—Colab will automatically prompt you for the two values when execution reaches the credential cell.

### Method C - Run locally

1. Create & activate a virtual environment

- macOS / Linux:
  ```bash
  python3 -m venv .venv
  source .venv/bin/activate
  python -m pip install --upgrade pip
  ```

- Windows (PowerShell):
  ```powershell
  python -m venv .venv
  .\.venv\Scripts\Activate.ps1
  python -m pip install --upgrade pip
  ```

2. Install dependencies

- If the repo has requirements.txt:
  ```bash
  pip install -r requirements.txt
  ```

- Otherwise (example):
  ```bash
  pip install requests pandas jupyterlab
  ```

3. Provide both credentials to the environment (do NOT hardcode)

- Temporary (session-only):

  - macOS / Linux:
    ```bash
    export NY_API_KEY_ID="your_application_key_id_here"
    export NY_API_KEY_SECRET="your_application_key_secret_here"
    jupyter notebook Task2.ipynb
    ```

  - Windows PowerShell:
    ```powershell
    $env:NY_API_KEY_ID = "your_application_key_id_here"
    $env:NY_API_KEY_SECRET = "your_application_key_secret_here"
    jupyter notebook Task2.ipynb
    ```

- Using a .env file (keep .env out of git):

  Create a `.env` file containing:
  ```
  NY_API_KEY_ID=your_application_key_id_here
  NY_API_KEY_SECRET=your_application_key_secret_here
  ```
  Add `.env` to `.gitignore` before use.

   Update the credential cell at the top of the notebook to read from `os.environ` when running outside Colab:

   ```python
   import os

   API_ID = os.environ.get("NY_API_KEY_ID")
   API_SECRET = os.environ.get("NY_API_KEY_SECRET")
   if not API_ID or not API_SECRET:
       raise RuntimeError("Missing NY_API_KEY_ID or NY_API_KEY_SECRET environment variables")
   ```

   Comment out the `from google.colab import userdata` import when using this fallback.

4. Run the notebook or script

- Launch Jupyter and run cells:
  ```bash
  jupyter notebook Task2.ipynb
  # or
  jupyter lab
  ```

- Or convert to a script:
  ```bash
  jupyter nbconvert --to script Task2.ipynb
  python Task2.py
  ```

5. Quick safety checklist

- Add `.env` and any secret files to `.gitignore`.  
- Never commit `NY_API_KEY_ID`, `NY_API_KEY_SECRET`, or other credentials.
- If a token is accidentally exposed, rotate it immediately.
