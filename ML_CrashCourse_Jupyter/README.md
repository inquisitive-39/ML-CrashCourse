# Jupyter Notebooks on Windows + WSL (Ubuntu) + VS Code

## Goal

Create a clean, professional Python and Jupyter development environment
where:

-   Windows runs the VS Code UI.
-   WSL Ubuntu runs Python, Jupyter and Git.
-   Every project has its own virtual environment (`.venv`).

Recommended project structure:

``` text
/home/wsl4home/projects/
└── ML_CrashCourse/
    ├── .venv/
    ├── notebooks/
    ├── data/
    ├── models/
    ├── requirements.txt
    └── .gitignore
```

## 1. Install WSL

In **PowerShell (Administrator)**:

``` powershell
wsl --install
```

Restart if prompted, launch Ubuntu and create your Linux
username/password.

Verify from **PowerShell** (not Ubuntu):

``` powershell
wsl --list --verbose
```

You should see `VERSION 2`.

## 2. Create your project

In the Ubuntu terminal:

``` bash
cd ~
mkdir -p projects
cd projects
mkdir ML_CrashCourse
cd ML_CrashCourse
```

Open in VS Code:

``` bash
code .
```

Ensure the bottom-left of VS Code says **WSL: Ubuntu**.

## 3. Install VS Code extensions

Install:

-   WSL (Microsoft)
-   Python (Microsoft)
-   Jupyter (Microsoft)

## 4. Update Ubuntu

``` bash
sudo apt update
sudo apt upgrade -y
```

## 5. Install Python tooling

``` bash
sudo apt install python3 python3-pip python3-venv git -y
```

Check Python:

``` bash
python3 --version
```

## 6. Create a virtual environment

``` bash
python3 -m venv .venv
```

Activate it:

``` bash
source .venv/bin/activate
```

Your prompt should begin with:

``` text
(.venv)
```

## 7. Upgrade pip

``` bash
python -m pip install --upgrade pip
```

## 8. Install Jupyter

``` bash
pip install jupyter notebook ipykernel
```

## 9. Install common ML packages

``` bash
pip install numpy pandas matplotlib scikit-learn
```

## 10. Register a Jupyter kernel

``` bash
python -m ipykernel install \
--user \
--name machine-learning \
--display-name "Python (Machine Learning)"
```

Check kernels:

``` bash
jupyter kernelspec list
```

## 11. Create folders

``` bash
mkdir notebooks data models
```

## 12. Open a notebook

Create `notebooks/intro.ipynb`.

Select:

-   **Python Environments**
-   Choose your `.venv` interpreter (or **Python (Machine Learning)** if
    listed)

Verify:

``` python
import sys
print(sys.executable)
```

Expected:

``` text
/home/wsl4home/projects/ML_CrashCourse/.venv/bin/python
```

## 13. Save dependencies

``` bash
pip freeze > requirements.txt
```

Reinstall later with:

``` bash
pip install -r requirements.txt
```

## 14. Create `.gitignore`

``` text
.venv/
__pycache__/
.ipynb_checkpoints/
*.pyc
```

## 15. Daily workflow

``` bash
cd ~/projects/ML_CrashCourse
source .venv/bin/activate
code .
```

## Useful commands

Current folder:

``` bash
pwd
```

Current Python:

``` bash
which python
```

Installed packages:

``` bash
pip list
```

Installed kernels:

``` bash
jupyter kernelspec list
```

Deactivate environment:

``` bash
deactivate
```

Delete virtual environment:

``` bash
rm -rf .venv
```

## Troubleshooting

### VS Code can't find the kernel

-   Ensure VS Code is running in **WSL: Ubuntu**.
-   Activate `.venv`.
-   Confirm:

``` bash
which python
jupyter kernelspec list
```

Reload VS Code using **Developer: Reload Window**.

### Notebook invalid JSON

Validate:

``` bash
python -m json.tool notebook.ipynb > /dev/null
```

If you receive a JSON error, inspect the notebook for corruption or
merge conflicts.

## Recommended workflow

1.  Write explanations in Markdown.
2.  Add equations using LaTeX.
3.  Use NumPy for calculations.
4.  Use Matplotlib to visualise concepts.
5.  Commit regularly with Git.
