
# 🚀 Automating Unit Testing with GitHub Actions

GitHub Actions for automated testing is a powerful tool for ensuring code integrity. In this guide, I'll explain how I automated the unit testing process for my **Flask-based** web app, **Personal Task Manager**, using GitHub Actions. This setup automatically runs tests on every push or pull request to ensure that any changes to the codebase don't break functionality.

🔗 **Check out the repository**:  
[Personal Task Manager - GitHub Repository](https://github.com/hamdan587/Personal-Task-Manager)

## 🛠️ Project Overview
The **Personal Task Manager** is a simple web app built with **Flask** that helps you manage your tasks. You can:
- Add, edit, delete, and complete tasks
- Set task priorities
- Store tasks in a `tasks.json` file

## ⚙️ GitHub Actions Setup

### 1️⃣ **Creating the Workflow File**

In the repository, I created a `.github/workflows/python-app.yml` file with the following content:

```yaml
name: Python Flask Application

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
      - name: Verify pytest installation
        run: |
          pip show pytest || pip install pytest
      - name: Run tests
        run: |
          pytest --maxfail=5 --disable-warnings
```

### 2️⃣ **How It Works**

- **Trigger**: Every time code is pushed to the `main` branch, or a pull request is made, GitHub Actions triggers the workflow.
- **Automation**: The workflow installs dependencies, ensures `pytest` is installed, and then runs the unit tests from `tests/test_task_manager.py`.

The status of the tests can be tracked in the **Actions** tab of the GitHub repository.

### ![Success Test Screenshot](https://github.com/hamdan587/Devops-Course-2024/blob/main/GithubAction.png)

## ✅ Running Tests Locally

To run the tests locally, use this command:

```bash
pytest tests/test_task_manager.py
```

## 💡 Key Takeaways

Through this small project, I’ve learned a great deal about how **DevOps concepts** like **GitHub Actions** can be leveraged to automate repetitive tasks like testing. Automation increases efficiency, scalability, and reliability—making workflows smoother and more error-free. I'm excited to continue learning and improving in this field, as automation and DevOps practices are essential to modern software development.

## 💬 Conclusion

By integrating **GitHub Actions** into the **Personal Task Manager** project, I was able to automate unit testing with each code change, ensuring that any new commits or pull requests are validated automatically. This approach not only improves productivity but also minimizes the risk of introducing bugs into the project.
