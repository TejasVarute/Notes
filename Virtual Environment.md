# Python Virtual Environment

- **Virtual environment** in python is an isolated environment on computer, where we can run and test python projects.
  - It allows to manage project-specific dependencies without interfering with other projects or original python installation.
  - It contains,
    - Has it own python interpreter.
    - Has it own set of installed packages.
    - Is isolated from other virtual enviroments.
    - Can have different versions of same package.
  - Importance,
    - It prevents package version conflicts between projects.
    - Makes project more protable and reproducible.
    - Keeps the system python installation clean.
    - Allows testing with different python versions.

## Steps to create virtual environment (venv) -

- Python has built in model `venv` for creating virtual environments.
- To create new virtual environment run following script/prompt on poweshell with admin access/command prompt,

```shell
> python -m venv [environment-name]
```

- This will create on folder named your given name [environment-name].
- Activate the environment using following prompt,

```shell
> [environment-name]\Scripts\activate
```

- After the environment activated, it shows the evironment name as follows on terminal,

```shell
([environment-name]) >
```
