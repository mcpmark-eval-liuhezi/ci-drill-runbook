# ci-drill-runbook

Throwaway public repo hosting a live-fire CI incident runbook drill.

## Workflows

- **Drill CI** (`.github/workflows/drill-ci.yml`) — triggered on `push` and `workflow_dispatch`; contains a job with a deliberate `exit 1` failure step to simulate a broken build.
- **Drill Soak** (`.github/workflows/drill-soak.yml`) — manual dispatch only; single job that sleeps for ~20 minutes.

## Drill steps

1. Push to `main` to kick off a red Drill CI run.
2. Capture the failed job log as evidence.
3. Open a tracking issue titled `CI drill: broken build on main` with the failed run id.
4. Dispatch the Drill Soak workflow and cancel it while it is in flight.
5. Re-run only the failed jobs of the Drill CI run.
6. Comment `DRILL COMPLETE` on the tracking issue.
