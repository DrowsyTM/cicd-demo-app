# CMPE 195B — CI/CD Demo App

A small Python/Flask app used in the **CI/CD & Deployment** class activity.

## What's in this repo

```
app.py              Flask web app with / and /health endpoints
src/calculator.py   Simple module with add, subtract, multiply, divide
tests/
  test_calculator.py  Unit tests for the calculator module
  test_app.py         Integration tests for the Flask routes
requirements.txt    All dependencies (flask, pytest, flake8, black, gunicorn)
Procfile            Tells Render/Heroku how to start the app
```

## Activity 1: Set Up CI

### 1. Fork or clone this repo

```bash
git clone <repo-url>
cd cicd-demo-app
```

### 2. Run the tests locally first

```bash
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt

pytest tests/ -v
```

All 10 tests should pass.

### 3. Run the linter locally

```bash
black --check app.py src/ tests/
flake8 app.py src/ tests/
```

Both should exit cleanly (no output = no errors).

### 4. Create the CI workflow

```bash
mkdir -p .github/workflows
```

Create `.github/workflows/ci.yml` using the template from the slides.

### 5. Push to a branch and open a PR

```bash
git checkout -b setup-ci
git add .github/workflows/ci.yml
git commit -m "Add CI workflow"
git push -u origin setup-ci
```

Open a PR on GitHub, then click the **Actions** tab to watch the pipeline run.

---

## Activity 2: Deploy

### Option A — Render

1. Push your repo to GitHub
2. Go to [render.com](https://render.com), sign in with GitHub
3. New → Web Service → connect this repo
4. Set:
   - **Build command:** `pip install -r requirements.txt`
   - **Start command:** `gunicorn app:app`
5. Deploy — visit your live URL and hit `/health`

### Option B — Vercel / Railway / Fly.io

The `Procfile` and `requirements.txt` are compatible with most Python PaaS platforms.

---

## Run locally (without Docker)

```bash
python app.py
# → http://localhost:5000
# → http://localhost:5000/health
# → http://localhost:5000/calculate/add/3/4
```
