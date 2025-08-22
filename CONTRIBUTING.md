# Contributing to Project Citadel

First and foremost, thank you for your interest in Project Citadel. We welcome contributions from the community. Your involvement is essential for the project's success.

This document provides a set of guidelines for contributing to the project. These are recommendations, not strict rules. We encourage you to use your best judgment and feel free to propose changes to this document in a pull request.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How to Contribute](#how-to-contribute)
  - [Reporting Bugs](#reporting-bugs)
  - [Suggesting Enhancements](#suggesting-enhancements)
  - [Submitting Pull Requests](#submitting-pull-requests)
- [Development Setup](#development-setup)
- [Pull Request Workflow](#pull-request-workflow)
- [Code Review Process](#code-review-process)

---

## Code of Conduct

This project and all participants are governed by the [Project Citadel Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report any unacceptable behavior.

---

## How to Contribute

There are many ways to contribute to the project, all of which are valuable.

### Reporting Bugs

If you encounter a bug, please help us by submitting a detailed report. Before creating a bug report, please check the existing issues to ensure the problem has not already been reported.

A good bug report should include:
* A clear and descriptive title.
* A step-by-step description of how to reproduce the issue.
* The expected behavior versus the actual behavior.
* Your operating system, Python version, and other relevant environment details.

### Suggesting Enhancements

If you have an idea for a new feature or an improvement, we encourage you to suggest it. Before creating an enhancement suggestion, please review the issue list to see if the idea has already been discussed.

A good enhancement suggestion should include:
* A clear and descriptive title.
* A detailed description of the proposed enhancement and the problem it solves.
* An explanation of why this enhancement would be useful to other users.
* Code examples or mockups, if applicable.

### Submitting Pull Requests

For direct contributions to the codebase, please follow the [Pull Request Workflow](#pull-request-workflow) detailed below.

---

## Development Setup

To get started with development, you will need to set up a local copy of the repository.

1.  **Fork the repository** on GitHub.
2.  **Clone your fork** to your local machine:
    ```sh
    git clone [https://github.com/your-username/citadel.git](https://github.com/your-username/citadel.git)
    cd citadel
    ```
3.  **Create a virtual environment** and install the project's dependencies.

---

## Pull Request Workflow

### Step 1: Create a New Branch

Create a dedicated branch for your changes. Use a descriptive prefix like `fix/`, `feature/`, or `docs/`.

```sh
git checkout -b your-branch-name
```
*Example: `git checkout -b feature/add-totp-support`*

### Step 2: Make and Test Your Changes

Write clean, readable code that adheres to the project's style. If you are adding a new feature or fixing a bug, please include tests that validate your changes.

### Step 3: Commit Your Changes

Commit your changes with a clear and descriptive commit message. We follow the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) specification.

```sh
git commit -m "feat: Add support for TOTP code generation"
```

### Step 4: Push to Your Fork

Push your changes to your forked repository on GitHub.

```sh
git push origin your-branch-name
```

### Step 5: Submit a Pull Request

Navigate to your forked repository on GitHub and open a new pull request.
* Fill out the pull request template with a detailed description of your changes.
* Reference any issues that your pull request resolves (e.g., "Fixes #123").

---

## Code Review Process

Once a pull request is submitted, it will undergo the following process:

1.  **Automated Checks:** The Continuous Integration (CI) pipeline will run automatically to ensure that all tests pass and the code meets our quality standards.
2.  **Code Review:** A project maintainer will review the code for correctness, style, and overall design. We aim to provide initial feedback within a few days.
3.  **Approval and Merge:** Once the pull request is approved and all checks have passed, a maintainer will merge it into the `main` branch.

Thank you for your contribution!
