# SliKube project plan

**Course deadline** December 1, 2026 at 11:59 p.m. CST. The team name, owners, and internal dates below are working assumptions for the team to confirm.

## Schedule and ownership

| Target | Proposed owner | Completion criteria |
| --- | --- | --- |
| Nov 20 | Dylan Walker | Confirm the team name and GitHub owner, initialize Git, and publish `TEAMNAME-FALL2026-SQA` as a public repository. Confirm each teammate’s email and complete the team row in the course spreadsheet. |
| Nov 20 | Josh Daniels | Run the baseline from a clean Python 3.11 environment with `yq` v4. Record dependency versions and the outcome of each starter test module. Identify the integration tests that need a portable local fixture. |
| Nov 24 | Nicholas Jebeles | Deliver `fuzz.py` with ten named targets, a repeatable seed, bounded case counts, behavior checks, and a summary of completed cases and confirmed bugs. |
| Nov 24 | Aubrey Foote | Add forensic logging to ten methods. Demonstrate the instrumentation with local fixtures and capture example logs. |
| Nov 27 | Josh Daniels | Update the starter GitHub Actions workflow. Verify a pull request and a push to the default branch run the selected tests, `python fuzz.py`, and a forensics smoke check. Save logs and capture screenshots. |
| Nov 29 | Dylan Walker with all teammates | Finish `SQA-REPO.md` with target lists, findings, evidence links, contributions, limitations, and lessons learned. Have a teammate verify the steps from a fresh clone. |
| Nov 30 | Dylan Walker | Verify the repository and report links are visible in a signed-out browser. Submit the public repository URL in Canvas and confirm the submission. |

The setup marks cover unpacking (1%), completing the team spreadsheet (1%), publishing the public repository (1%), and listing the team in the repository README (2%). Confirm teammate emails for the spreadsheet. [Official assignment and team spreadsheet](docs/assignment.md)

## Fuzzing (25%)

Use local generated inputs for ordinary behavior checks in `fuzz.py`. For each target, document the expected behavior, run deterministic cases and seeded variations, and record the number of cases exercised. Include the seed and a short description of any unexpected result in the report. Use a nonzero exit status for unexpected harness failures so Actions can surface them.

| Module | Candidate targets | Behavior checks |
| --- | --- | --- |
| `parser.py` | `checkIfWeirdYAML`, `checkIfValidHelm` | Path classification on synthetic strings. |
| `parser.py` | `keyMiner`, `getKeyRecursively`, `getValuesRecursively`, `getValsFromKey` | Expected paths, values, and depths on bounded nested dictionaries and lists. |
| `parser.py` | `update_json_paths`, `getSingleDict4MultiDocs` | Path normalization and merge behavior on generated YAML-shaped data. |
| `graphtaint.py` | `constructHelmString`, `getValidTaints` | String construction and mapping on synthetic tuples. |

## Forensics (25%)

Instrument ten methods with standard Python logging. Include an event name, run identifier where available, method, outcome, and counts or duration where meaningful. Use sanitized fixture names or relative paths when needed. Keep manifest contents and secret values out of logs. Compare the instrumented run with the baseline to verify that return values and output formats remain consistent.

| Module | Candidate methods |
| --- | --- |
| `main.py` | `main` |
| `parser.py` | `checkIfValidK8SYaml`, `checkIfValidHelm`, `loadMultiYAML` |
| `scanner.py` | `runScanner`, `getYAMLFiles`, `scanSingleManifest`, `scanForSecrets` |
| `graphtaint.py` | `getMatchingTemplates`, `getValidTaints` |

Use a small local fixture set that exercises all ten methods. Record the fixture, command, and events that show each method ran.

## Continuous integration (25%)

1. Begin with `python -m unittest TEST_PARSING`, then run `TEST_GRAPH`, `TEST_SCANNING`, and `TEST_INTEGRATION` individually to establish their baseline results. The starter integration tests reference an author’s absolute path in `TEST_CONSTANTS.py`. Make that coverage portable with repository fixtures and derive the expected results from those fixtures before requiring it in CI.
2. Update `.github/workflows/python.build.yml` for pull requests and default-branch pushes. Install verified Python dependencies and the required `yq` version. Run the applicable tests, fuzzing, and the forensics smoke check as separate visible steps.
3. Preserve test, fuzzing, and forensic logs on failed and successful runs. Include a representative sanitized log and screenshot for each of the three activities in the public repository. Link to the corresponding workflow run from the report.

## Report and submission (20% for the report)

Complete [SQA-REPO.md](SQA-REPO.md) with the methods covered, repeatable commands, findings, workflow outcomes, and lessons learned. Verify that the public repository name matches the assignment format, the root README lists the team, the course spreadsheet is complete, and the code, logs, and screenshots are reachable. One teammate submits the repository URL in Canvas.
