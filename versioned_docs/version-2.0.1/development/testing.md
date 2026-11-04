---
sidebar_position: 2
title: Running Tests
---

# Running Tests

IntelliKeep uses `pytest` for backend testing.

## Run via Docker (recommended)

No local Python installation required.

```bash
# All tests
./run-tests.sh

# Specific file
./run-tests.sh tests/test_task_manager.py

# With filter
./run-tests.sh -k test_complete_recurring
```

By default, the tests run against the current Home Assistant release. To test against the oldest supported line (2026.2.x), use the Python 3.13 image:

```bash
PYTHON_IMAGE=python:3.13-slim ./run-tests.sh
```

## Run locally

The current Home Assistant needs Python 3.14 or later.

```bash
pip install -r requirements_test.txt
pytest tests/ -v
```

## Test structure

Tests live in the `tests/` directory of the IntelliKeep repository. The suite covers:
- Task creation, update, completion, reopening and deletion
- Recurring task scheduling: repeat intervals, the schedule anchor, weekdays, month ends and daylight-saving changes
- The to-do list and calendar entities
- Notification trigger conditions
- Service action validation

## Continuous integration

GitHub Actions runs the tests on Python 3.14 (current Home Assistant) and Python 3.13 (Home Assistant 2026.2.x) on every push and pull request, and once a week to catch breakage from new Home Assistant releases. HACS validation, `hassfest` and a frontend build also run on pushes and pull requests to `main`.
