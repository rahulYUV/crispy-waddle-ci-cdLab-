# crispy-waddle-ci-cdLab

## Q. Configure automatic code integration between GitHub and GitHub Actions for continuous deployment

## Theory
GitHub Actions is a cloud-based CI/CD service that runs automated workflows directly from your GitHub repository, so no separate Jenkins installation is required.

## Step by Step
1. Push this project to a GitHub repository.
2. Open the repository on GitHub.
3. Go to the `Actions` tab and allow workflows if GitHub asks.
4. Add the workflow file from this project at `.github/workflows/deploy.yml`.
5. Make sure the repository has GitHub Pages enabled.
6. In repository settings, set Pages source to `GitHub Actions`.
7. Push a commit to the `main` branch.
8. GitHub Actions will run automatically on every push.
9. The workflow will package the static site into `dist/` and deploy it to GitHub Pages.

## Pipeline Flow
- Checkout code from GitHub
- Validate project files
- Package the static app into `dist/`
- Deploy the packaged output to GitHub Pages

## Result
This practical demonstrates automatic code integration and continuous deployment without installing Jenkins.
