# Contributing to Risk Analysis System

Thank you for considering contributing to the Risk Analysis Syatem! This document outlines the development and deployment process, including setup instructions, CI/CD configurations, and branching strategy.

## Table of Contents

1. [Getting Started](#getting-started)
   - [Prerequisites](#prerequisites)
   - [Installation](#installation)
   - [Setting Up the Development Environment](#setting-up-the-development-environment)
2. [Development Workflow](#development-workflow)
   - [Branching Strategy](#branching-strategy)
   - [Code Style and Linting](#code-style-and-linting)
   - [Running Tests](#running-tests)
3. [CI/CD Pipeline](#cicd-pipeline)
   - [Continuous Integration](#continuous-integration)
   - [Continuous Deployment](#continuous-deployment)
4. [Deployment Instructions](#deployment-instructions)
   - [Heroku Deployment](#heroku-deployment)
   - [AWS Elastic Beanstalk Deployment](#aws-elastic-beanstalk-deployment)
5. [Reporting Issues](#reporting-issues)
6. [Submitting Pull Requests](#submitting-pull-requests)

## Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- **Python 3.x**: Required for running the application.
- **pip**: Python package manager.
- **git**: Version control system.
- **Heroku CLI** (if deploying to Heroku).
- **AWS CLI** (if deploying to AWS Elastic Beanstalk).

### Installation

1. **Clone the repository**:

    ```bash
    git clone https://github.com/MALVMAS/RAS.git
    cd MALVMAS
    ```

2. **Create a virtual environment**:

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3. **Install dependencies**:

    ```bash
    pip install -r requirements.txt
    ```

### Setting Up the Development Environment

1. **Configure environment variables**:

    Create a `.env` file in the root of your project and add the necessary environment variables:

    ```plaintext
    DEBUG=True
    SECRET_KEY=your-secret-key
    DATABASE_URL=your-database-url
    ```

2. **Run the development server**:

    ```bash
    python manage.py runserver
    ```

## Development Workflow

### Branching Strategy

We follow the **GitFlow** branching model:

- **main**: The main branch contains the production-ready code.
- **develop**: The development branch is where the latest development happens.
- **feature/***: Feature branches are created from `develop` for new features.
- **hotfix/***: Hotfix branches are created from `main` to address critical issues.

### Code Style and Linting

We use `autopep8` and `pycodestyle` to enforce code style:

- Run the linter:

    ```bash
    pycodestyle your_module/
    ```

- Auto-format code:

    ```bash
    autopep8 --in-place --aggressive --aggressive your_module/
    ```

### Running Tests

We use `pytest` for testing:

- Run all tests:

    ```bash
    pytest
    ```

## CI/CD Pipeline

### Continuous Integration

We use **GitHub Actions** for continuous integration:

- The CI pipeline runs automatically on every push to the `main` and `develop` branches.
- It installs dependencies, runs tests, and checks code quality.

Example CI configuration (`.github/workflows/ci.yml`):

```yaml
name: CI Pipeline

on:
  push:
    branches:
      - main
      - develop
  pull_request:
    branches:
      - main
      - develop

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.x'
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
```
    - name: Run tests
      run: pytest

### Continuous Deployment
We use Heroku or AWS Elastic Beanstalk for automatic deployments:

The deployment pipeline triggers after a successful build on the main branch.
#### Heroku Deployment
Deployment to Heroku is configured in the CI pipeline:

deploy:
  runs-on: ubuntu-latest
  needs: test
  steps:
  - uses: actions/checkout@v2
  - name: Deploy to Heroku
    env:
      HEROKU_API_KEY: ${{ secrets.HEROKU_API_KEY }}
    run: |
      git remote add heroku https://git.heroku.com/<your-heroku-app>.git
      git push heroku main


## Deployment Instructions
### Heroku Deployment
1. **Install Heroku CLI:**
curl https://cli-assets.heroku.com/install.sh | sh
2. **Login to Heroku:**
heroku login
3. **Deploy manually (if needed):**
git push heroku main

### AWS Elastic Beanstalk Deployment
1. **Install AWS CLI:**
   pip install awscli
2. **Configure AWS CLI:**
   aws configure
3. **Deploy manually (if needed):**
   eb deploy

## Reporting Issues
If you encounter any issues or bugs, please open an issue in the GitHub repository. Provide as much detail as possible, including steps to reproduce the issue.

## Submitting Pull Requests
1. **Fork the repository.**
2. **Create a new branch: git checkout -b feature/your-feature-name.**
3. **Commit your changes: git commit -m 'Add some feature'.**
4. **Push to the branch: git push origin feature/your-feature-name.**
5. **Open a pull request in the GitHub repository.**

Please ensure your pull request adheres to the following guidelines:

- Include tests that cover your changes.
- Follow the code style guidelines.
- Ensure that all tests pass before submitting.

Thank you for contributing to the Risk Analysis System Project!
