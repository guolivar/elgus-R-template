# `secrets/`

* Credentials and other sensitive files go in here: API keys, tokens, database connection
  details, service account files
* **Nothing in this folder is committed.** `.gitignore` excludes the whole folder apart
  from this `README.md`
* Because it isn't committed, this folder won't exist for anyone who clones the project so
  list below what a collaborator needs to put here and where to get it
* Never hard-code a secret in a script in `R/` or `python/`. Read it at runtime instead,
  for example:

```r
# For environment variables
readRenviron("secrets/.Renviron")
api_key <- Sys.getenv("API_KEY")
# For dataframe based usage
credentials_service1 <- read.delim("secrets/secrets_service1.txt",delim = ";")
```

```python
from dotenv import load_dotenv
import os

load_dotenv("secrets/.env")
api_key = os.environ["API_KEY"]
```

* Don't print a secret to the console or into a report — it ends up in `.Rhistory`, in
  knitted output in `docs/`, and in logs
* Files matching `_secret*` anywhere in the project are also ignored, as is `.httr-oauth`

## What belongs here

_TODO — replace with the files this project expects, for example:_

| File | Contains | Where to get it |
|------|----------|-----------------|
| `.Renviron` | `API_KEY` for the data provider | Project owner |
