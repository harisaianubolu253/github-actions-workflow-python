# GitHub Actions Lab 1.1: Pull Request CI for JavaScript and Python

## Lab Objective

In this lab, students learn how GitHub Actions runs continuous integration checks on a pull request before code is merged into `main`.

The repository demonstrates:

- JavaScript linting with ESLint.
- JavaScript testing with Node.js built-in test runner.
- Python linting with flake8.
- Python testing with pytest.
- Reading workflow logs.
- Finding failed jobs and failed steps.
- Debugging common lint and test failures.

This project is intentionally small so beginners can focus on CI concepts instead of application complexity.

## Prerequisites

Students should have:

- A GitHub account.
- Git installed.
- Node.js 22 installed locally if they want to run the JavaScript demo on their machine.
- Python 3.12 installed locally if they want to run the Python demo on their machine.
- A code editor such as Visual Studio Code.
- Basic command line comfort in Windows PowerShell, Git Bash, Linux, or macOS.

## Folder Structure

```text
github-actions-lab-1.4/
├── javascript-demo/
│   ├── package.json
│   ├── eslint.config.js
│   ├── index.js
│   └── index.test.js
├── python-demo/
│   ├── app.py
│   ├── test_app.py
│   └── requirements.txt
├── .github/
│   └── workflows/
│       ├── javascript-pr-checks.yml
│       └── python-pr-checks.yml
└── README.md
```

## Difference Between Linting and Testing

Linting checks code style and catches common programming mistakes before the code runs.

Examples:

- Unused variables.
- Missing semicolons.
- Incorrect indentation.
- Lines that are too long.

Testing runs code and checks whether it behaves correctly.

Examples:

- `add(2, 3)` should return `5`.
- A function should raise an error for invalid input.
- A web API should return the expected response.

In this lab, linting answers "Is the code clean?" and testing answers "Does the code work?"

## What Is a GitHub-Hosted Runner?

A GitHub-hosted runner is a temporary virtual machine provided by GitHub to run workflow jobs.

In these workflows, the runner is defined with:

```yaml
runs-on: ubuntu-latest
```

That means GitHub creates a fresh Ubuntu machine, checks out the repository, installs the requested language version, runs the commands, saves the logs, and then removes the machine after the job finishes.

## Step-by-Step Setup

1. Create a new empty repository on GitHub.
2. Clone the repository to your computer.

   ```bash
   git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
   cd YOUR-REPOSITORY
   ```

3. Copy the contents of this lab into the repository root.
4. Commit the starter project.

   ```bash
   git add .
   git commit -m "Add GitHub Actions Lab 1.4 starter project"
   git push origin main
   ```

5. Confirm that these workflow files exist in GitHub:

   ```text
   .github/workflows/javascript-pr-checks.yml
   .github/workflows/python-pr-checks.yml
   ```

The workflows run on pull requests targeting `main`, so they will not run from the initial push to `main`.

## Run the Checks Locally

JavaScript:

```bash
cd javascript-demo
npm install
npm run lint
npm test
```

Return to the repository root:

```bash
cd ..
```

Python:

```bash
cd python-demo
python -m pip install -r requirements.txt
flake8 .
pytest -v
```

On some systems, the Python command may be `python3` instead of `python`.

## Create a Branch and Pull Request

1. Create a feature branch.

   ```bash
   git checkout -b feature/ci-demo
   ```

2. Make a small change, such as editing this README.
3. Commit and push the branch.

   ```bash
   git add .
   git commit -m "Practice pull request checks"
   git push origin feature/ci-demo
   ```

4. Open the repository on GitHub.
5. Click **Compare & pull request**.
6. Set the base branch to `main`.
7. Create the pull request.
8. Watch the GitHub Actions checks run on the pull request page.

## How to Read GitHub Actions Logs

1. Open the pull request on GitHub.
2. Scroll to the checks section.
3. Click **Details** next to a workflow.
4. Select the failed or successful job on the left.
5. Expand each step to see the commands and output.

Each workflow in this lab has a clear sequence:

JavaScript:

- Check out repository.
- Set up Node.js.
- Install dependencies.
- Run ESLint.
- Run JavaScript tests.

Python:

- Check out repository.
- Set up Python.
- Install dependencies.
- Run flake8.
- Run pytest.
