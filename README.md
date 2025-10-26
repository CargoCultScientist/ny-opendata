# Task 2 - Run instructions

This repository contains instructions to run the existing script that retrieves the last 10 additions from the target registry via the SODA API. Do not refactor or rename anything; the script’s API naming is the source of truth. Keep SODA parameter names as-is: `$limit`; `$order`; `$select`; `$where`; header `X-App-Token`.

## Open in Colab

Run in the browser; zero local setup.

[Open in Colab](https://colab.research.google.com/#create=true)

This opens a fresh notebook. Upload your script file exactly as it exists in the repo, then set your token and run it.

## Get the API key from the source

This dataset is hosted on a Socrata Open Data portal. Anonymous requests work for small pulls; using an Application Token raises rate limits.

1. Sign in to the portal that hosts the dataset.
2. Go to your account or developer settings and create an Application Token.
3. Copy the token value. In this project we store it as an environment variable named `NY_API_KEY` to match the screenshot and the existing code.

Reference: [Socrata Application Tokens](https://dev.socrata.com/docs/app-tokens.html)

## Insert the token in Colab

Choose one method. Do not change your script.

### Method A - Colab Secrets panel

1. In Colab, open the left sidebar; click the key icon labeled Secrets.
2. Add a secret named **NY_API_KEY** with your token value; enable Notebook access for the current notebook.
3. Load it into the environment so your script can read it.

### Method B - Secure prompt inside the notebook

Insert a new cell: 

'''python
import os, getpass
os.environ["NY_API_KEY"] = getpass.getpass("Paste your Application Token: ")
'''

Then run the remaining script.

### Method C - Run locally

If you want to run this locally, you know what to do. 
Just please use venv and don't hardcode your credentials in the script. 

