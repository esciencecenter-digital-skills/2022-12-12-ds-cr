![](https://i.imgur.com/iywjz8s.png)


# Collaborative Document: Good Practices in Research Software Development (Code Refinery)

2022-12-12-ds-cr day 4

Welcome to The Workshop Collaborative Document.

This Document is synchronized as you type, so that everyone viewing this page sees the same text. This allows you to collaborate seamlessly on documents.


## 👮Code of Conduct

Participants are expected to follow these guidelines:
* Use welcoming and inclusive language.
* Be respectful of different viewpoints and experiences.
* Gracefully accept constructive criticism.
* Focus on what is best for the community.
* Show courtesy and respect towards other community members.

## 🎓 Certificate of attendance

If you attend the full workshop you can request a certificate of attendance by emailing to training@esciencecenter.nl .

## ⚖️ License

All content is publicly available under the Creative Commons Attribution License: [creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/).

## 🙋Getting help

To ask a question, raise your hand in zoom. Click on the icon labeled "Reactions" in the toolbar on the bottom center of your screen,
then click the button 'Raise Hand ✋'. For urgent questions, just unmute and speak up!

You can also ask questions or type 'I need help' in the chat window and helpers will try to help you.
Please note it is not necessary to monitor the chat - the helpers will make sure that relevant questions are addressed in a plenary way.
(By the way, off-topic questions will still be answered in the chat)


## 🖥 Workshop website

[link](https://esciencecenter-digital-skills.github.io/2022-12-12-ds-cr/)

🛠 Setup

[link](https://esciencecenter-digital-skills.github.io/2022-12-12-ds-cr#setup)

## 👩‍🏫👩‍💻🎓 Instructors

Barbara Vreede, Sven van der Burg, Leon Oostrum

## 🧑‍🙋 Helpers

Luisa Orozco, Dani Bodor

## 🗓️ Agenda
| Time | Topic |
|--:|:---|
| 9:00 | 	Welcome and icebreaker |
| 9:15 | Introduction to testing |
| 10:15 | Coffee break |
| 10:30 | Introduction to Continuous Integration |
| 11:30 | Coffee break |
| 11:45 | More advanced testing |
| 12:45 | Wrap-up |
| 13:00 | END |



## 🔧 Exercises

### Prep for today's work: clone this repository

```bash
git clone git@github.com:bvreede/temperature_plotting.git
cd temperature_plotting
git remote rm origin
```

### Exercise: write a test for the following function:

```python!
def create_name(num):
    name = f"plot_{str(num)}.png"
    return name
```

- use multiple different inputs, and verify their output
- write different kinds of assertions (e.g. assert the output, but also the type of output, etc.)
- include a test for an error

### If you have time left and want a challenge:
#### Bonus exercise 1:
Write a test for any of the other functions in the codebase

#### Bonus exercise 2:
Write a failing test. Then improve the code so it no longer fails.
Please share in your answer below not just the (no longer failing) test, but also the updated code!


## Excercise on GitHub action:
- Edit `tests/test_temperature_plotting.py` so that it fails. What interesting thing do you notice on GitHub site?

For example:

```python=
def test_compute_mean_bad():
    calc = tpl.compute_mean([1,2,3])
    assert calc == 5
```

After a short while, you should now see a red cross appearing (instead of the green check we saw earlier) because the tests now fails. You can take a detailed look at what step failed by clicking the cross.


## 🧠 Collaborative Notes

### Tests
```bash
conda activate coderefinery
pytest
```
Pytest should run, although there is nothing to test yet. But it should not crash.

Open a jupyter notebook  in the same folder as the repo that you downloaded :
```python!
import pytest
import temperature_plotting as plt

def test_compute_mean():
    calc = tpl.compute_mean([0, 10, 20])
    assert calc == 10 # test if the answer is the expected
    assert type(calc) == float # test if the type of the answer is the one expeced

    calc = tpl.compute_mean([-10, 10])
    assert calc == 0 # test special cases (negative numbers)

    calc = tpl.compute_mean([0, 10, 0])
    # assert calc == 3.33 # this would fail because the exact result is 3.333333333.......
    assert round(calc,4) == 3.3333, "Check that the average is roughly correct" # displays a message if an error

    with pytest.raises(TypeError) as e: # asserts that this particular error type will occur
        calc = tpl.compute_mean(["a", "b", "c"]) # this would fail, because the function does not work with strings
    assert e is not None, "We should not be able to average strin"

    calc = tpl.compute_mean([])
    assert calc == None # this failed in original function definition, so we will change it (see below)


test_compute_mean()
```

We will adjust the `compute_mean()` function to ensure that empty lists return None

```python!
def compute_mean(data):
    """Compute the mean of a list of numbers
    Args:
        data (list): a list of numbers
    Returns:
        float: the mean value of the list
    """

    if len(data) == 0:
         return None
    else:
        mean = sum(data)/ len(data)
        return mean
```

Tests are integral part of your code (as the documentation). You should create independent files containing your tests and place them a folder `tests` in your repository (the exact name of this folder is important).


Unit tests check at a detailed level whether everything works as intended, and if not where it goes wrong
Integration tests check at a higher level that the entire codebase works, as opposed to checking that the code does exactly what you expect at the unit level.
These tests are complimentary and are both very useful


```python!
# integration test
import os

def test_main()
    tpl.main()
    assert os.path.exists("plot_25.png")

test_main()
```

Save the jupyter notebook as a script in the same folder of the repo, subfolder `tests` and give it a descriptive name: `test_temperature_plotting.py`. Ensure that the filename starts with `test_` and is a python file ()

In your terminal run the following (make sure you are in the environment coderefinery):
```bash
touch tests/__init__.py # creates an empty file with name __init__.py
pytest
```
This should now not give any errors.


### Continuous integration (CI)
The idea of continuous integration is to automate all the tests we have been doing instead of doing it manually. We will now work in GitHub.
Create an empty repository on the GitHub site, make sure it is completely empty (all boxes to auto create files shoukd be unchecked!), because we have a local repo.
copy/paste from GitHub and run in bash: `git remote add origin git@github.com:<YourName>/<RepoName>.git`

- Check that the command `git status` shows "On branch main".
- Check that `git remote -v` shows origin. If it says something different run `git remote rm origin`

```bash
git push --set-upstream origin main
```

GitHub actions are things you can run on your repo.
Go to the "Actions" tab on your repo url. Then click configure on the "Python application" box.
This will create a premade file that already has a lot of the things you want, but we will adjust it to our needs.

### Explanation of the sections:
name: name of the workflow
on: which action workflow to be activated (e.g., when pushing or creating a PR)
jobs:
    build:
        runs-on: which OS to use
        steps: step-by-step actions
          uses: actions defined externally (don't worry about these too much)
          name: name of the action (for troubleshootinh)
          with: which python version to use (ensure you put quotations marks around "3.10", otherwise it will be read as 3.1)
          run: the actual command you want to run (if you want to run multiple lines, add a | (vertical bar) and then the separate commands below each other with the same indentation )
          shell: you can specify a (non-default) shell (e.g. bash, when using windows)

### What's next
- create the yaml file via GitHub button
- the repo will now show a little orange button in your repo, next to latest commit , indicating that the tests are running. This will turn into a green checkmark once they pass (or a red cross if anything fails)
- if someone want to collaborate with you and creates a pull request, these actions will run immediately (assuming you left pull-request in the "on" section). This way you can make sure that they did not accidentally break anything when trying to improve your code.

Edit file `.github/workflows/python-app.yml`. (In Github you can click on the edit button at the right top).
at `-name: Install dependencies` add `shell: bash`.
Rename `build` --> `test`: We will see now that the name of the run in the Github Actions Tab changes.
We will skip the failing test from the excercise by add a decorator (a special python command) in the line just above the function: `@pytest.mark.skip(reason="test is bad")`

Test on more than 1 platform (Windows, Ubuntu, Mac) and multiple python versions (3.9 and 3.10)
Modify `.github/workflows/python-app.yml`

```bash!
...
jobs:
  test:
    strategy:
      matrix:
        os: [windows-latest, macos-latest, ubuntu-latest]
        python-version: ['3.9', '3.10']
      fail-fast: false # this will force to run all of the combinations despite errors in one of them

    runs-on: ${{ matrix.os }}

    steps:
    - uses: actions/checkout@v3
    - name: Set up Python ${{ matrix.python-version }}
      uses: actions/setup-python@v3
      with:
        python-version ${{ matrix.python-version }}
...
```

The entire test file will run 6 times:
- on Windows, ubuntu and MacOS
- on python version 3.9 and 3.10 for each

### Documentation in Github page
We want to add SPhinx documentation to Github repo.
Make sure any changes you made remotely (on Github site) are pulled to your local repo.
Also make sure you are still in the coderefinery environment (`conda activate coderefinery`)

```bash=
git pull
mkdir doc
cd doc
sphinx-quickstart # Fill in some details about the project.
# there are now a bunch of new files/folders inside doc
nano conf.py # or use your favorite editor
html_theme = 'sphinx_rts_theme' # change the theme
nano index.rst
# Remove Indices and tables section

sphinx-build . _build  # build in doc folder


# add docs to remote
git add Makefile
git add conf.py
git add index.rst
git add make.bat
git commit -m "add documentation"
git push

# open site
open _build/index.html # in Mac
start _build/index.html # on Windows
sensible-browser _build/index.html # on ubuntu


```

*Note:* We don't want to add `_build` folder, only the source files. We want this files to be generated automatically on Github or locally (if you want to build the docs locally).

Edit file `.github/workflows/python-app.yml`. Create a new section with just one OS, so that it does not create the docs multiple times.

```bash=
# Add section
jobs:
  docs:
    runs-on: ubuntu-latest
    needs: test # or whatever you called the other block. this line causes the section to only run if the other section passed

    # intermediate part should be similar to the tests section.

    - name: Build documentation #Every new step starts with a - (be carful with indentation)
      run: sphinx-build doc _build
    - name: Publish documentation
      uses: peaceiris/actions-gh-pages@v3
      with:
        publish_branch: gh-pages # which branch it uses
        publish_dir: _build # where is the documentation going to be generated
        github_token: ${{ secrets.GITHUB_TOKEN }}
```
Remove the permissions section from the yml file.

In `requirements.txt` Sphinx is listed, so it is installed during "Install dependencies".
You will have to modify some repository settings to generate the token tath is going to be used.

If you want to build the documentation **only** if the tests have passed: in section `docs:` add `needs: test`.

The file `conf.py` in [Leon's repo](https://github.com/loostrum/temperature_plotting/) :
```python=
# Configuration file for the Sphinx documentation builder.
#
# This file only contains a selection of the most common options. For a full
# list see the documentation:
# https://www.sphinx-doc.org/en/master/usage/configuration.html

# -- Path setup --------------------------------------------------------------

# If extensions (or modules to document with autodoc) are in another directory,
# add these directories to sys.path here. If the directory is relative to the
# documentation root, use os.path.abspath to make it absolute, like shown here.
#
# import os
# import sys
# sys.path.insert(0, os.path.abspath('.'))


# -- Project information -----------------------------------------------------

project = 'Temperature plotting'
copyright = '2022, Barbara & Leon'
author = 'Barbara & Leon'


# -- General configuration ---------------------------------------------------

# Add any Sphinx extension module names here, as strings. They can be
# extensions coming with Sphinx (named 'sphinx.ext.*') or your custom
# ones.
extensions = [
]

# Add any paths that contain templates here, relative to this directory.
templates_path = ['_templates']

# List of patterns, relative to source directory, that match files and
# directories to ignore when looking for source files.
# This pattern also affects html_static_path and html_extra_path.
exclude_patterns = ['_build', 'Thumbs.db', '.DS_Store']


# -- Options for HTML output -------------------------------------------------

# The theme to use for HTML and HTML Help pages.  See the documentation for
# a list of builtin themes.
#
html_theme = 'sphinx_rtd_theme'

# Add any paths that contain custom static files (such as style sheets) here,
# relative to this directory. They are copied after the builtin static files,
# so a file named "default.css" will overwrite the builtin "default.css".
html_static_path = ['_static']
```

### Activate GitHub Pages
Go to the settings of your repo -> pages, and there select Source: Deploy from a branch. Select branch `gh_branch`.
Then you can go to the documentation of the repo: `username.github.io/repository_name` (just type this in your browser).


### Add docstrings to documentation
in terminal:

```bash=
git pull # make sure all remote changes are copied to local
cd .. # make sure
cd doc
nano index.rst

# in nano
.. toctree::
   :maxdepth: 2
   :caption: Contents:

   api.rst
# save and exit nano

nano api.rst

# in nano
The API
======= #make sure it's the same length as the title

.. automodule:: temerature_plotting # no .py at end!
    :members:

nano conf.py
#remove # from lines in section # --Path setup
import os
import sys
sys.path.insert(0, os.path.abspath('..'))

#in section #-- General configuration
extensions = ['sphinx.ext.autodoc']
```
**rst** stands for restructured text.
**API** stands for Application Programming Interface

Commit and push your changes -> it will trigger the generation of the documentation.


## Link to working final repo:
https://github.com/loostrum/temperature_plotting


## 📚 Resources

- [A participant recommended this video](https://www.youtube.com/watch?v=CFRhGnuXG-4) as a motivation to make code more modular
- Github [documentation] (https://docs.github.com/en/actions/automating-builds-and-tests/about-continuous-integration) about Continuous integrations
- [Guide for creating your own github runners](https://github.com/ci-for-research/self-hosted-runners) #GPU.
- [Post-workshop survey](https://www.surveymonkey.com/r/TGDXZ36)
- [Link to the repo with testing and documentation set up:](http://github.com/loostrum/temperature_plotting/actions)