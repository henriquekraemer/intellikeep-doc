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

## Run locally

```bash
pip install -r requirements_test.txt
pytest tests/ -v
```

## Test structure

Tests are located in the `tests/` directory of the IntelliKeep repository. The test suite covers:
- Task creation, update, completion, and deletion
- Recurring task scheduling logic
- Notification trigger conditions
- Service action validation
