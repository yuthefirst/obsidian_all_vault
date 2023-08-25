# Create virtual environments

1. Pip install the Virtual Environment
```shell
pip install virtualenv
```

2. Create the virtual environments
```bash
 python<version> -m venv <virtual-environment-name>
```
e.g:
```bash
mkdir projectA
 cd projectA
 python -m venv env
```

3. Active the virtual environment
```bash
source env/bin/activate
```

4. PIP install requirement.txt
```bash
pip install -r requirements.txt
```

5. Deactivate a Virtual Environment
```shell
deactivate
```
