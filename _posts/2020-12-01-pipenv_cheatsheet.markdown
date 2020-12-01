---
layout: single
title:  "Pipenv Cheatsheet"
date:   2020-12-01
comments: false
---

## Introduction

Pipenv uses pip for package management and virtualenv for maintaining virtual environment under the hood. It works as a wrapper and uses same kind of syntax to make it easy to work.

You can more or less forget about using pip and virtualenv if you are using `pipenv`.

> pip install pipenv

## Cheatsheet

> Activate/Deactivate Environment

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv shell</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Activate</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">exit</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Deactivate</span>

> Locate environment

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv --venv </span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// locates for a particular project</span>

> Delete environment

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv --rm</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// This will not remove the Pipfiles</span>

> Install/Uninstall/Update Packages

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv install flask</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// If virtual environment doesn't exist, it'll create it</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv install flask==0.12.1</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Installs specific version</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv install pytest --dev</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// To separate dev packages from production environment</span>

---

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv uninstall flask</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Uninstalls package</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv uninstall --all</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Uninstalls all packages</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv uninstall --all-dev</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Uninstalls all dev packages</span>

---

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv update package_name </span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Update specific package</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv update</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Updates all packages</span>

> Create/Update the lock file

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv lock </span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Done usually before pushing the code</span>

> To install from Pipfile

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv install --dev </span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// installs from pipfile along with dev pacakges; creates environment if not present; updates packages if version not mentioned</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv install </span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// doesn't install dev packages; creates environment if not present; updates packages if version not mentioned</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv install --ignore-pipfile </span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// installs from lock file; ccreates environment if not present; updates packages if version not mentioned</span>

## Extra Features

> Install/Export requirements.txt

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv install -r requirements.txt </span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// installs a list of requirements</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv lock -r > requirements.txt </span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// export a list of requirements</span>

> Create environment with specific python version

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv shell --python 3.5 </span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// will use python 3.5 now</span>

> Open Third Party Package

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv open requests </span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// opens code in default editor; to open in vscode use environment variable EDITOR=code</span>

> Run in Environment without opening Shell

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv run <insert command here> </span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// e.g pipenv run python app.py</span>

> Check Security Vulnerabilities

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv check</span>

> List Packages and their Dependencies

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv graph</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// to resolve conflicting sub-dependencies use `pipenv graph --reverse`</span>