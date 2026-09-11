# Setting Up a Python Dev Environment on Linux

A practical, step-by-step guide to a clean, modern Python setup.

## 1. System Packages

Update the system and install the essentials:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y python3 python3-pip python3-venv git curl build-essential
```

| Package | Purpose |
|---------|---------|
| `python3` | The Python interpreter |
| `python3-venv` | Creates isolated virtual environments |
| `build-essential` | Compiler tools needed by some Python packages |
| `git` | Version control |

Check your versions:

```bash
python3 --version
pip3 --version
```

## 2. Managing Python Versions (Optional)

Distributions ship a system Python — leave it untouched. To install a different version, use **pyenv**:

```bash
curl https://pyenv.run | bash
# add to ~/.bashrc:
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
```

Then install any Python version:

```bash
pyenv install 3.12.0
pyenv global 3.12.0
```

## 3. Virtual Environments

Isolate project dependencies with a virtual environment (`venv`):

```bash
mkdir my_project && cd my_project
python3 -m venv .venv
source .venv/bin/activate     # activate
```

Your prompt changes to `(.venv)`. Now `pip install` only affects this project.

```bash
pip install requests            # install a package
pip freeze > requirements.txt    # save dependencies
pip install -r requirements.txt  # restore dependencies
```

To exit the environment:

```bash
deactivate
```

## 4. Package Management with pip

Install packages from [PyPI](https://pypi.org):

```bash
pip install numpy pandas matplotlib
pip install --upgrade pip
```

Track dependencies in `requirements.txt` to keep your project reproducible.

## 5. Code Editor

Two popular choices:

### VS Code

```bash
sudo snap install code --classic
```

Install the **Python** and **Pylance** extensions for autocomplete, linting, and debugging.

### PyCharm

```bash
sudo snap install pycharm-community --classic
```

## 6. Recommended Tools

| Tool | Purpose | Install |
|------|---------|---------|
| `ruff` | Fast linter & formatter | `pip install ruff` |
| `pytest` | Testing framework | `pip install pytest` |
| `black` | Code formatter | `pip install black` |
| `ipython` | Enhanced interactive shell | `pip install ipython` |

## 7. Project Structure

A clean layout for a new project:

```
my_project/
├── .venv/              # virtual environment (gitignore this)
├── .gitignore
├── requirements.txt    # dependencies
├── README.md
└── src/                # your Python code
    └── main.py
```

`.gitignore` should include:

```
.venv/
__pycache__/
*.pyc
```

## 8. Git Setup

```bash
git init
git add .
git commit -m "Initial commit"
```

## Summary Checklist

1. ✅ Install Python, pip, venv, git
2. ✅ Create a virtual environment per project
3. ✅ Track dependencies in `requirements.txt`
4. ✅ Use a modern editor (VS Code or PyCharm)
5. ✅ Add linters/formatters (ruff, black)
6. ✅ Write tests with pytest
7. ✅ Use git for version control
