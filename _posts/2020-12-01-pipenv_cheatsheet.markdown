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

> _Activate/Deactivate Environment_

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv shell</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Activate</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">exit</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Deactivate</span>

> Delete environment

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv --rm</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// This will not remove the Pipfile</span>

> Install/Uninstall/Update Packages

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv install flask</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// If virtual environment doesn't exist, it'll create it</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv install flask==0.12.1</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Installs specific version</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv uninstall flask</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Uninstalls package</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv install pytest --dev</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// To separate dev packages from production environment</span>

```By default, if someone installs your packages from Pipfile, the dev packages will be ignored. To install dev packages as well, `--dev` flag has to be used.```

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv update</span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Updates all packages</span>

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">pipenv update <package_name> </span> &emsp;
<span style="color: yellow;background-color: #1E242C;font-size:13px; font-family: 'Lucida Grande'">// Update specific package</span>

> 