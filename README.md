## CI/CD (GitHub Actions)

This repository uses GitHub Actions to run a CI/CD pipeline for the TypeScript monorepo.

### CI (Pull Requests)
On every pull request, the pipeline:
- Installs dependencies using `pnpm` with a locked install (`--frozen-lockfile`)
- Runs lint checks
- Runs TypeScript type checking
- Runs unit tests
- Runs build steps (to ensure the repo compiles before merge)

These checks are required before merging to `main`.

### CD (Main Branch)
On pushes to `main`, the pipeline:
- Re-runs validation (install/lint/typecheck/test/build)
- Optionally publishes packages (if using Changesets)
- Optionally deploys applications (e.g., Docker/Kubernetes/Vercel), depending on environment configuration

### Performance
The pipeline uses dependency caching and task-level caching (e.g., Turborepo/Nx) to reduce build times by only re-running work that changed.
