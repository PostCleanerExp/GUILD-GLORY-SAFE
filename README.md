# Guild Glory Safe — Render deployment

This repository packages the optimized Render build. The app serves its dashboard at `/`, exposes `/health`, reads Render's `PORT`, and stores runtime data under `/var/data`.

Set `DASHBOARD_PASSWORD` in Render before using the dashboard. Deploy with the included Render Blueprint.
