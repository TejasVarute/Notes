# Python Virtual Environment

- **Virtual environment** in python is an isolated environment on computer, where we can run and test python projects.
  - It allows to manage project-specific dependencies without interfering with other projects or original python installation.
  - It contains,
    - Has its own python interpreter.
    - Has its own set of installed packages.
    - Is isolated from other virtual environments.
    - Can have different versions of same package.
  - Importance,
    - It prevents package version conflicts between projects.
    - Makes project more portable and reproducible.
    - Keeps the system python installation clean.
    - Allows testing with different python versions.

## Steps to create virtual environment (venv) -

- Python has built in module `venv` for creating virtual environments.
- To create new virtual environment run following script/prompt on powershell with admin access/command prompt,

```shell
> python -m venv [environment-name]
```

- This will create a folder named your given name [environment-name].
- Activate the environment using following prompt,

```shell
> [environment-name]\Scripts\activate
```

- After the environment activated, it shows the environment name as follows on terminal,

```shell
([environment-name]) >
```

## Deactivate Virtual Environment

- To exit the virtual environment, simply run:

```shell
> deactivate
```

---

## Managing Dependencies

- **Exporting dependencies**
  - To save the list of installed packages to a file (usually `requirements.txt`).

```shell
> pip freeze > requirements.txt
```

- **Installing dependencies**
  - To install packages from a `requirements.txt` file.

```shell
> pip install -r requirements.txt
```

---
