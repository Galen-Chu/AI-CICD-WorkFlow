# ⚙️ AI-CICD-WorkFlow

> Continuous Integration / Continuous Deployment pipeline scaffold.

---

## 🏗️ Pipeline · 管線

```
[Push / PR] → Lint (flake8) → Test (pytest) → Docker Build → Deploy
```

---

## 📁 Structure · 結構

| Path | Purpose |
|------|---------|
| `src/app.py` | Minimal Flask app (`/`, `/health`) |
| `tests/` | pytest test suite |
| `Dockerfile` | Container image build |
| `.github/workflows/ci-cd.yml` | Pipeline definition |
| `.flake8` | Lint configuration |
| `.dockerignore` | Docker build exclusions |

---

## 🚀 Local Development · 本地開發

```bash
pip install -r requirements-dev.txt
flake8 src tests
pytest -v
python -m src.app
```

---

## 🐳 Docker

```bash
docker build -t ai-cicd-workflow .
docker run -p 8000:8000 ai-cicd-workflow
```

---

## 🚢 Deploy · 部署

The `deploy` job in `.github/workflows/ci-cd.yml` only runs on pushes to `main`
after lint, test, and docker-build all pass. Replace the placeholder step with
your actual deployment (SSH, registry push, cloud provider CLI, etc.) and store
any credentials as GitHub Actions secrets — never commit them.

For a full CI/CD toolkit with lint, test, build, deploy, and rollback scripts,
see [program-g-code](https://github.com/Galen-Chu/program-g-code).

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Galen Chu**

- GitHub: [@Galen-Chu](https://github.com/Galen-Chu)
- LinkedIn: [Galen Chu](https://www.linkedin.com/in/galen-chu-203590b5/)
