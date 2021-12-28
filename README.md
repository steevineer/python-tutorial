# python-tutorial

## Installation (MacOS for now)

- Open `Terminal.app` for the following steps: 
- Install `Homebrew`, for further info visit https://brew.sh/ 
```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
- Install `Python`
```sh
brew install python
```
- Check new `python`
```
python3 --version

## Should show Python 3.9.9
```

## Visual Studio Code

- Install `vscode` as code editor
```sh
brew install visual-studio-code
```
- Create and open a workspace with `vscode`
```
mkdir -p ~/dev/mypy
code ~/dev/mypy
```
- Check out some basic setups for `vscode` https://code.visualstudio.com/docs/editor/codebasics
- Install plugin for `python` tooling within `vscode` https://marketplace.visualstudio.com/items?itemName=ms-python.python

## Python Virtual Environment

- Development for a `python` app usually requires downloading variety of third-party modules. 
- It is helpful to have isolated enviroment for each app, since no app created equal. 
- Press `ctl ~` to open a terminal within `vscode`
- Create a `virtual-env` from the location of the above workspace
```
python3 -m venv ~/dev/mypy/myenv
```
- At this point `vscode` might recognize the presence of the new `virtual-env` and ask to activate. Once activated, reopen the terminal in `vscode` might show the `(myenv)` in front of the prompt signaling it's activated.
- To manually activate `virtual-env`: 
```
source ~/dev/mypy/myenv/bin/activate
```
- Use `deactivate` to exist the `virtual-env`

## Initialize Django 
- Create a `requirement.txt` file in the workspace location to download modules for `django` with following content:
```
Django>=3.0,<4.0
shortuuid>=1.0.1
gunicorn
```
- Make sure the `virtual-env` is activated, run following command in terminal to fetch the required modules:
```
pip install -r requirements.txt
```
- Generate a new `django` app at the same location of workspace:
```
django-admin startproject mysite
```
- Test run the `app` locally:
```
cd mysite
python manage.py runserver

## Should show ...Starting development server at http://127.0.0.1:8000/...
```
- Open the browser at localhost:8000 to see the running website.

## Create Polling App

- For detail https://docs.djangoproject.com/en/4.0/intro/tutorial01/#creating-the-polls-app
