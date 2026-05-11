# crispy-waddle-ci-cdLab

## Q. Configure automatic code integration between GitHub and GitHub Actions for continuous deployment

## Theory
GitHub Actions is a cloud-based CI/CD service that runs automated workflows directly from your GitHub repository, so no separate Jenkins installation is required.

## Pipeline Flow
- Checkout code from GitHub
- Validate project files
- Package the static app into `dist/`
- Deploy the packaged output to GitHub Pages

## Result
This practical demonstrates automatic code integration and continuous deployment without installing Jenkins.
