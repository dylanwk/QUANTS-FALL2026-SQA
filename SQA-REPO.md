# SliKube SQA report

## Baseline

The starter archive was unpacked and its 94 files were accounted for. All Python source files compiled with Python 3.13.13, with three existing regex escape warnings in `parser.py`. The dependency install could not resolve packages in the setup environment, so the CLI and parser tests stopped at missing imports. The assignment baseline will use Python 3.11 and `yq` v4 as described in the [setup instructions](README.md#local-setup).

Record the tested commit, dependency and `yq` versions, and the result of each test module after running the baseline.

## Fuzzing

List the ten methods, input generation and expected behavior, seeds, case counts, and confirmed bugs. Include the command and link the fuzz log and screenshot.

## Forensics

List the ten instrumented methods, event fields, sample fixtures, and verification results. Include the command and link the forensic log and screenshot.

## Continuous integration

Describe the workflow triggers and jobs. Link the workflow file, a representative Actions run, and its logs and screenshots.

## Lessons learned and contributions

Summarize what the team learned, what each person contributed, and any remaining limitations.
