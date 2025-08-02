# Contributing to plan-engine

First off, thanks for taking the time to contribute! We welcome improvements, bug fixes, tests, and documentation enhancements.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Code of Conduct](#code-of-conduct)
3. [How to Contribute](#how-to-contribute)

   * [Reporting Issues](#reporting-issues)
   * [Suggesting Enhancements](#suggesting-enhancements)
   * [Submitting Pull Requests](#submitting-pull-requests)
4. [Development Workflow](#development-workflow)

   * [Branching Model](#branching-model)
   * [Commit Message Guidelines](#commit-message-guidelines)
   * [Writing Tests](#writing-tests)
5. [Style and Quality](#style-and-quality)
6. [Local Testing](#local-testing)
7. [Release Process](#release-process)
8. [License](#license)

---

## Getting Started

1. Fork the repository.
2. Clone your fork:

   ```bash
   ```

git clone [https://github.com/your-org/plan-engine.git](https://github.com/your-org/plan-engine.git)
cd plan-engine

````
3. Install dependencies (see `README.md`):
   ```bash
poetry install
````

4. Create a feature branch:

   ```bash
   ```

git checkout -b feature/my-new-feature

```

## Code of Conduct

This project follows the [Contributor Covenant Code of Conduct](CODE_OF_CONDUCT.md). Please ensure you read and follow it.

## How to Contribute

### Reporting Issues

If you find a bug or have a feature request, please open an issue:
1. Check for existing issues to avoid duplicates.
2. Fill out the issue template with:
   - A clear description of the problem or feature.
   - Steps to reproduce (for bugs).
   - Expected vs. actual behavior.

### Suggesting Enhancements

Enhancement requests should include:
- A clear description of the enhancement.
- Use cases or user stories.
- Any relevant context (e.g., links, screenshots).

### Submitting Pull Requests

1. Fork the repo and create a branch from `main`.
2. Commit your changes in logical, atomic commits.
3. Push your branch to your fork.
4. Open a PR against `main` with:
   - A descriptive title.
   - Summary of changes.
   - Issue reference (if applicable).

## Development Workflow

### Branching Model

- `main` branch is always production-ready.
- Create feature branches from `main`:
  - `feature/<short-description>` for new features.
  - `bugfix/<short-description>` for bug fixes.
  - `docs/<short-description>` for documentation-only changes.

### Commit Message Guidelines

Follow the [Conventional Commits](https://www.conventionalcommits.org/) spec:
```

<type>(<scope>): <subject>

<body>

<footer>
```
- **type**: `feat`, `fix`, `docs`, `chore`, `style`, `refactor`, `test`.
- **scope**: optional component or file impacted.
- **subject**: short summary (<50 chars).
- **body**: detailed description.
- **footer**: references issues (#123) or breaking changes.

### Writing Tests

* Add unit tests for new features or bug fixes.
* Use pytest conventions.
* Keep tests deterministic and stateless.
* Aim for high coverage in core logic (chains, tools, API schemas).

## Style and Quality

* Follow PEP 8 for Python code.
* Run `black .` and `flake8` before committing.
* Document public functions and classes with docstrings.
* Update `CHANGELOG.md` for user-facing changes.

## Local Testing

```bash
pytest --maxfail=1 --disable-warnings -q
```

Ensure all tests pass before opening a PR.

## Release Process

Releases are managed via GitHub releases and follow Semantic Versioning (SemVer).

1. Bump version in `pyproject.toml`.
2. Update `CHANGELOG.md`.
3. Tag the commit (`vX.Y.Z`).
4. Push and create a GitHub release.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
