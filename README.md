# AI-CICD-WorkFlow

Continuous Integration / Continuous Deployment pipeline scaffold.

```
[Push / PR] -> Lint (flake8) -> Test (pytest) -> Docker Build -> Deploy
```

## Structure

- `src/app.py` — minimal Flask app (`/`, `/health`)
- `tests/` — pytest test suite
- `Dockerfile` — container image build
- `.github/workflows/ci-cd.yml` — pipeline definition

## Local development

```bash
pip install -r requirements-dev.txt
flake8 src tests
pytest -v
python -m src.app
```

## Docker

```bash
docker build -t ai-cicd-workflow .
docker run -p 8000:8000 ai-cicd-workflow
```

## Deploy

The `deploy` job in `.github/workflows/ci-cd.yml` only runs on pushes to `main`
after lint, test, and docker-build all pass. Replace the placeholder step with
your actual deployment (SSH, registry push, cloud provider CLI, etc.) and store
any credentials as GitHub Actions secrets — never commit them.
