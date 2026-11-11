# Guild Glory Safe — Render build

The project now serves `index.html` and the dashboard API from one Render web service.

## Render deployment

1. Push this project to GitHub and create a Render **Web Service** from that repository.
2. The included `render.yaml` selects the 512 MB paid plan (`0.5c-512mb`) and mounts a 1 GB persistent disk at `/var/data`. This is the always-on plan configuration; the Free plan sleeps after 15 minutes without inbound traffic and cannot attach a persistent disk.
3. Set `DASHBOARD_PASSWORD` in Render → Environment to a strong password (at least 16 characters). The dashboard's API remains locked until this is set.
4. Deploy. Open the service's `https://<service-name>.onrender.com/` address. The root route serves `index.html`; `/health` is the health-check endpoint.

Render supplies `PORT`; the app binds to `0.0.0.0:$PORT` (with `10000` as the local fallback). Do not enter a port in the browser URL. Open the generated `https://<service-name>.onrender.com/` URL; the root route serves `index.html` directly.

Paid instances do not spin down for inactivity, but deploys, maintenance, or infrastructure incidents can still interrupt a process. This is not an uptime SLA.

## 512 MB tuning

The defaults limit account generation to 6 accounts, 2 generator threads, and 4 active workers. Start with fewer accounts and check Render's memory graph before increasing `MAX_ACTIVE_ACCOUNTS`, `MAX_GENERATOR_ACCOUNTS`, or `MAX_GENERATOR_THREADS`.

## Data and secrets

Runtime files (`accounts.json`, archived accounts, token cache, device profiles, guild settings, and logs) are written under `DATA_DIR`. On Render this is `/var/data`, so they survive deploys/restarts while the persistent disk is attached. Do not commit real accounts, passwords, tokens, or generated caches. The `.gitignore` excludes them.

The uploaded source bundle contained an account archive with plaintext passwords and a device profile file. Those machine/account-specific files were deliberately left out of this deployable source package; the app will create fresh runtime files as needed. Never commit these files to a public repository.

## Local run

```bash
python -m venv .venv
. .venv/bin/activate
pip install -r requirements.txt
export DASHBOARD_PASSWORD='use-a-long-random-password-here'
python -u app.py
```

Then open `http://127.0.0.1:10000/`.
