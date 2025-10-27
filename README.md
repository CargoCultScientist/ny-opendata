# Task 2 - Run instructions

This repository contains instructions to run the existing script that retrieves the last 10 additions from the target registry via the SODA API.

## Open Task2.ipynb in Colab (one-click)

Run in the browser — no local setup required.

Open the notebook directly in Google Colab (this link opens the notebook from this repository and commit):

[Open Task2.ipynb in Colab](https://colab.research.google.com/github/CargoCultScientist/ny-opendata/blob/93c2d69e8453c19756dcb8a4229acb5e5c9d34e0/Task2.ipynb)

## Get the API key from the source

This dataset is hosted on a Socrata Open Data portal. Anonymous requests work for small pulls; using an Application Token raises rate limits.

1. Sign in to the portal that hosts the dataset.  
2. Go to your account or developer settings and create an Application Token.  
3. Copy the token value. In this project, we store it as an environment variable named `NY_API_KEY` to match the screenshot and the existing code.

Reference: [Socrata Application Tokens](https://dev.socrata.com/docs/app-tokens.html)

## Insert the token in Colab

Choose one method.

### Method A - Colab Secrets panel

1. In Colab, open the left sidebar and click the key icon labeled "Secrets".  
2. Add a secret named **NY_API_KEY** with your token value and enable Notebook access for the current notebook.  
3. Load it into the environment so your script can read it.

### Method B - Secure prompt inside the notebook

Insert a new cell:

```python
import os, getpass
os.environ["NY_API_KEY"] = getpass.getpass("Paste your Application Token: ")
```

Then run the remaining cells.

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
  pip install requests sodapy jupyterlab
  ```

3. Provide the NY_API_KEY to the environment (do NOT hardcode)

- Temporary (session-only):

  - macOS / Linux:
    ```bash
    export NY_API_KEY="your_application_token_here"
    jupyter notebook Task2.ipynb
    ```

  - Windows PowerShell:
    ```powershell
    $env:NY_API_KEY = "your_application_token_here"
    jupyter notebook Task2.ipynb
    ```

- Using a .env file (keep .env out of git):

  Create a `.env` file containing:
  ```
  NY_API_KEY=your_application_token_here
  ```
  Add `.env` to `.gitignore` before use.

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
- Never commit `NY_API_KEY` or other credentials.  
- If a token is accidentally exposed, rotate it immediately.
