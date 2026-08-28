# lift-log

A personal, read-only workout dashboard hosted on GitHub Pages. The repository is the source of truth: merged pull requests are the write path.

## Workflow

1. Create a branch from `main`.
2. Edit `data/workouts.json`, update `updatedAt`, and add a workout or personal record.
3. Open a pull request (for example, `workout: 2026-08-28 push day`).
4. Merge the PR. GitHub Actions redeploys the static site.

There is deliberately no browser write access, server, database, token, or login. This keeps a personal site safe to publish and makes every change auditable in Git history. GitHub Pages is free for public repositories (and available for private repositories subject to GitHub plan limits).

## Data shape

Each workout has an ISO date, a name, and sets with `exercise`, `weightKg`, and `reps`. Records are optional objects such as:

```json
{ "exercise": "Barbell bench press", "value": 100, "unit": "kg", "metric": "1RM", "date": "2026-08-28", "prUrl": "https://github.com/moenn1/lift-log/pull/1" }
```

The UI calculates total volume as the sum of weight × reps. It is a training log, not medical advice.

## GitHub Pages

Pages must be enabled once by a repository administrator; GitHub does not allow the normal workflow token to create the Pages site automatically. In repository **Settings → Pages**, select **GitHub Actions** as the source, save, and rerun the workflow. The workflow in `.github/workflows/pages.yml` uploads the repository as a static artifact and deploys it whenever `main` changes. For private repositories, Pages availability depends on your GitHub plan; making this personal repository public is the simplest free option.

## Dataset

The exercise names were inspired by [exercises-dataset](https://github.com/hasaneyldrm/exercises-dataset). Its README describes MIT-licensed data and separately attributed media; this project does not redistribute the dataset's images or GIFs.
