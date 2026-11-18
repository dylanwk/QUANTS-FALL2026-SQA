# QUANTS — Fall 2026 Software Quality Assurance

**Team name** QUANTS  
**Course** COMP 5710/6710  
**Public repository name** `QUANTS-FALL2026-SQA`

## Team

- Nicholas Jebeles
- Dylan Walker
- Aubrey Foote
- Josh Daniels

SliKube is the starter project for this assignment.

## Local setup

Use Python 3.11, the version specified by the starter environment. Install [Mike Farah’s `yq` v4](https://mikefarah.gitbook.io/yq/) and make it available on `PATH` for scans that look up YAML line numbers.

```bash
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
yq --version
python main.py --help
python -m unittest TEST_PARSING
```

The tests expect to be run from the repository root, where `TEST_ARTIFACTS/` is available. See the [project plan](PROJECT-PLAN.md) for the baseline checks and integration-test fixture gap.

## Course documents

- [Assignment handout](docs/assignment.md)
- [Project plan](PROJECT-PLAN.md)
- [SQA report](SQA-REPO.md)
- [Original starter README](docs/starter-readme.md)
