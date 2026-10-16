# EPİAŞ Market Clearing Price Explorer

A small Streamlit interface for retrieving a selected day's Market Clearing Price (PTF/MCP) from the EPİAŞ Transparency Platform through the external `eptr2` client.

The repository's contribution is the date-driven UI, credential lookup, request handling and table display in `get_mcp_data.py`. The API client is an upstream dependency; this repository does not implement the EPİAŞ API.

## Flow

Date selection → Streamlit secrets → `EPTR2.call("mcp", start_date=..., end_date=..., postprocess=True)` → DataFrame/list normalization → displayed table. Empty and failed responses produce UI feedback. This is a data viewer; it places no market orders.

## Run locally

Use Python 3.10+ and your own EPİAŞ access credentials:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
streamlit run get_mcp_data.py
```

Create an untracked `.streamlit/secrets.toml`:

```toml
[eptr_credentials]
EPTR_USERNAME = "your-username"
EPTR_PASSWORD = "your-password"
```

Choose a date and click **Fetch Data**. Credentials are read by the server; never commit or share this secrets file. Dependencies are currently unpinned, so a successful installation/API check is still needed before selecting a reproducible lock.

## Validation and scope

The source passed a syntax check. No authenticated EPİAŞ request or Streamlit browser session was run. There are no assertions of live API compatibility or data freshness. Error messages currently include upstream exception details and should be reviewed before shared hosting. Caching, export and a chart are follow-up work. No project-wide license is declared.
