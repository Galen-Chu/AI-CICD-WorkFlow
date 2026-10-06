# ⚙️ AI-CICD-WorkFlow

> Continuous Integration / Continuous Deployment pipeline scaffold.

---

## 🏗️ Pipeline · 管線

```
[Push / PR] → Lint (ruff) ┐
                          ├→ Docker Build → Push to GHCR (main only) → Deploy (pull + smoke test)
          → Test (pytest + coverage) ┘
```

Lint 與 Test 平行執行；Docker 映像檔以 commit SHA 為 tag 推送到 GHCR，
deploy job 會拉取同一���映像檔並對 `/health` 做 smoke test 後才繼續部署。

---

## 📁 Structure · 結構

| Path | Purpose |
|------|---------|
| `src/app.py` | Minimal Flask app (`/`, `/health`) |
| `tests/` | pytest test suite |
| `Dockerfile` | Container image build |
| `.github/workflows/ci-cd.yml` | Pipeline definition |
| `.github/dependabot.yml` | Weekly dependency updates (pip / actions / docker) |
| `ruff.toml` | Lint + format configuration |
| `.dockerignore` | Docker build exclusions |

---

## 🚀 Local Development · 本地開發

```bash
pip install -r requirements-dev.txt
ruff check src tests        # lint
ruff format --check src tests  # format check（ruff format 可自動修正）
pytest -v --cov=src         # 測試 + 覆蓋率
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
after lint, test, and docker-build all pass. `docker-build` pushes the image to
`ghcr.io/<owner>/<repo>:<sha>` using the built-in `GITHUB_TOKEN`（首次推送會自動建立
private package）。`deploy` 拉取同一個映像檔、驗證 `/health` 後才執行部署 ——
把 placeholder step 換成實際部署（SSH、cloud provider CLI 等），憑證一律存在
GitHub Actions secrets，切勿 commit 進 repo。

若 deploy 拉取映像檔時出現權限錯誤，到 GitHub 套件頁面 → Package settings →
Manage Actions access，把此 repo 加入並授權 Read 即可。

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
