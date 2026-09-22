# Raqib Fraud Detection Service — Lab 5 Solution (SDA-AIE-113)

## What this is

This repository contains the **Lab 5** — "Build the Pipeline" (CI/CD
with GitHub Actions) implementation on top of the completed Lab 1–4 service. It already contains a **complete, working Lab 1 +
Lab 2a + Lab 3 + Lab 4 solution**: the FastAPI service, the Docker/compose
setup, AND the full three-level pytest suite are all implemented and
passing.

If you finished Lab 4 yourself with a working result, keep using your
own repo instead of this one. This starter exists so nobody falls behind
— everyone begins Lab 5 from the same known-good baseline.

## What already works (Lab 1 through Lab 4, done for you)

```
src/fraud_service/            # domain/service/adapters/api — all implemented
Dockerfile, docker-compose.yml, requirements.lock, scripts/startup_time.sh
payloads/malformed/             # 40-file malformed-payload corpus
tests/
├── conftest.py                  # ConstantModel, client_factory, real_model, sample_txn
├── unit/test_policies.py          # 6-case tightened decision-band test
├── integration/test_predict_api.py  # contract + malformed corpus + no-stack-trace + readiness
└── behavioural/test_model_behaviour.py  # invariance + directional + 5,000-row golden file
scripts/regen_golden.py           # regenerates the golden file — a deliberate, reviewed step only
BENCHMARKS.md                       # Day 1 + Lab 3 + Lab 4 numbers already filled in
```

```
$ make test
52 passed in ~2s (fast suite, ~99% branch coverage)

$ pytest -m slow
3 passed in ~6s (behavioural suite, real model, golden file)
```

## Lab 5 implementation

```
.github/workflows/ci.yml    # lint, test, image-smoke, publish jobs
payloads/sample.json        # valid smoke-test payload
pyproject.toml              # import-linter clean-architecture contract
BENCHMARKS.md                # Day 3 Lab 5 timing table (fill after GitHub runs)
```

The remaining part is a **GitHub-side task**: this lab needs your fraud-service repository
actually pushed to GitHub with Actions enabled — CI cannot run against a
local-only folder. If you don't already have this repo on GitHub:

```
git init   # if not already a repo (this starter already is one)
gh repo create fraud-service --private --source=. --push
# or create an empty repo on github.com and:
git remote add origin <your-repo-url>
git push -u origin main
```

Full step-by-step instructions, expected results, and a troubleshooting
table are in the Day 3 Lab Guide (Lab 5 section) — work through it in
order; this README is just the starting-point map.

## Quick start

```
pip install -e ".[dev,api]"
make test              # 52 fast tests, all green
pytest -m slow         # 3 behavioural tests, all green
make up && make smoke  # Docker stack, from Lab 3
```
