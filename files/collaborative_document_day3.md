![](https://i.imgur.com/iywjz8s.png)


# Collaborative Document: Good Practices in Research Software Development (Code Refinery)

2022-12-12-ds-cr day 3

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

### 🛠 Setup

[link](https://esciencecenter-digital-skills.github.io/2022-12-12-ds-cr#setup)

### ⬇️ Download files:

Run:
```bash!
wget https://raw.githubusercontent.com/coderefinery/modular-type-along/master/data/temperatures.csv
```

Or by [right clicking here > Save Link As](https://raw.githubusercontent.com/coderefinery/modular-type-along/master/data/temperatures.csv). (Make sure the file is a .csv.)


## 👩‍🏫👩‍💻🎓 Instructors

Barbara Vreede, Sven van der Burg, Leon Oostrum

## 🧑‍🙋 Helpers

Luisa Orozco, Dani Bodor

## 🗓️ Agenda
| Time | Topic |
|--:|:---|
| 9:00 | Welcome and icebreaker |
| 9:15 | Writing modular code |
| 10:15 | Coffee break |
| 10:30 | Writing modular code |
| 11:00 | Documentation |
| 11:30 | Coffee break |
| 11:45 | Documentation |
| 12:45 | Wrap-up |
| 13:00 | END |

## :snowflake: Ice breaker

## 🔧 Exercises

### Documentaton wishlist

- What the code does, how it does, and what it does need to be run, author, title, description
- explain 'smart' pieces of code
- describe what each block of code is doing, with input and output details/formats
- code examples of the API
- argument descriptions of functions/methods +1
- architecture overview if it is a bigger package
- reproducibility & replicability (sorry if it is evident - not many archaeologists are doing this...): so meta information on the dataset
- commented code: what is it for + explain - show what is going on in your brain + examples and tutorial for the documentation
- purpose of the code +1
- To help users understand the code and further use it and develop.
- how to use the code/examples. name and contact of the developer(s). dependencies.
- Describe what a piece of code does.
- Describe the format of input and outpd output arguments
- Which package versions are needed (i.e., which versions were used to build a working version of the code)
- All functions should clearly state input and output variables
- Summary of what a function/module does
- Functions should be clear to understand
- What input/output a module/function has
- Describe how
- Document todo's on collaborative projects for other contributors.

### Exercise: Think of good and bad examples
Write down your thoughts in the collaborative documents.
Respond with emojis :+1: :scream_cat: to your colleagues' answers.
- Think of projects of which you like the documentation. What do you like about them?
- Think of projects for which you don’t like the documentation. What don’t you like about them? Are you missing anything?

**NB: You can choose a mature library with lots of users for this exercise, but try to also think of less mature projects you had to collaborate on, or papers you had to reproduce.**

#### Good examples of documentation

- https://umap-learn.readthedocs.io/en/latest/ -- lot's of examples and also good API documentation
- Bioconductor::ComplexHeatmap package documentation: https://jokergoo.github.io/ComplexHeatmap-reference/book/ Well structured, logical flow of the documentation book, example codes that works
- stars https://r-spatial.github.io/stars/
- [Seaborn](https://seaborn.pydata.org/generated/seaborn.heatmap.html)
- https://keras.io/api/e but actually using a package cis super different generally speaking
- (Papyrus scripts - Github)[https://github.com/OlivierBeq/Papyrus-scripts] Well structured, how to install with troubleshooting options, GoogleCollab tutorials. Very complete for a small scale project!
- Xarray documentation https://docs.xarray.dev/en/stable/
- https://fmriprep.org/en/stable/ > like their examples + FAQ
- OceanParcels: has a tutorial in Jupyter notebook which you can easily execute (without writing anything yourself). Makes it very comprehensive how to use the code.: https://oceanparcels.org/
- https://github.com/nedap/deidentify (offers a quick setup and works very well off-the-shelf)

#### Bad examples of documentation

- Seaborn https://seaborn.pydata.org/generated/seaborn.heatmap.html ;p 😲; Agreed
- scipy.optimize.curve_fit https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.curve_fit.html - the behaviour with a (k,M) sized xdata is never explained
- https://numpy.org/doc/stable/reference/generated/numpy.where.html Depending on your use this function, the result is either a single array or a tuple with multiple arrays. This is not properly described in the documentation and there are no examples of this behaviour.
- BISICLES ice sheet model http://davis.lbl.gov/Manuals/BISICLES-DOCS/index.html it is mostly undocumented and there are very little examples.
- https://docs.anaconda.com/ (too many things in one place and nondescriptive links, hard to search)


## 🧠 Collaborative Notes

### Writing modular code

#### What is modularity?
- It is a way to organize and structure code.
- Plus: Increases readability, testability,
**Building blocks** should have sub-blocks roughly of the same size.

Hierarchy (from small to big): functions - classes - modules - libraries - programs

Open up the terminal of your choice/OS.

```bash=
mkdir plot_demo
cd plot_demo
```

Download the files: instructions in section ⬇️ Download files

```bash=
wget https://raw.githubusercontent.com/coderefinery/modular-type-along/master/data/temperatures.csv
ls # should show temperatures.csv
```

Activate the environment. If you're on windows: open your Anaconda navigator -> Anaconda prompt or.

```bash=
conda activate coderefinery
jupyter-lab # Should open jupyter-lab in your browser
```

Save your notebook, copy-paste:
```python!
import pandas as pd
from matplotlib import pyplot as plt

num_measurements = 25

# read data from file
data = pd.read_csv("temperatures.csv", nrows=num_measurements)
temperatures = data["Air temperature (degC)"]

# compute statistics
mean = sum(temperatures) / num_measurements

# plot results
plt.plot(temperatures, "r-")
plt.axhline(y=mean, color="b", linestyle="--")
plt.show()
plt.savefig("25.png")
plt.clf()
```

Jupyter notebooks use literate programming (programming with text). They are vry nice to make for example tutorials, examples, demos. It s

Add axis labels with the following code:
```python!
plt.xlabel("measurements")
plt.ylabel("air temperature (deg C)")
```

Improve the code to plot also 25, 100 and 500 measures.
Indent the code that read the file and plot results.
Delete the definition line of num_measurements.
Then add a for loop:
```python!
for num_measurements in [25, 100, 500]:
```
But the axis labels appear only for the for the first plot, not the 2 other.

We can define a function with common code for all `num_measurements`
```python!
def plot_temperatures(temperatures):
    plt.plot(temperatures, "r-")
    plt.axhline(y=mean, color="b", linestyle="--")
    plt.show()
    plt.savefig(f"{num_measurements}.png")
    plt.clf()
```
and then, replace the code that did the same in the loop for a call to function `plot_temperatures`
```python!
plot_temperatures(temperatures)
```
Now we can re-use this function whenever we neded it.

**Global variable:** Available for all scopes.
**Local variable:** Only exists inside the function, but it is notn possible to access it from outside the function where it was defined.

We can make a function that calculates the mean -> Can help improve the readability of the code.

```python!
def compute_statistics(data):
    mean = sum(data) / len(data)
    return mean
```
and then, we can replace the line where we calculated the mean with a call to the function:
```python!
compute_statistics(temperatures)
```
Another chunk that can be separated is the process of reading the data, we can create the function:
```python!
def read_data(file_name, num_measurements, colname):
    data = pd.read_csv(file_name, nrows=nrows)
    data_read = data[colname]
    return data_read
```
and then we can modify the main code to only call the function:
```python!
temperatures = read_data("temperatures.csv",
                         num_measurements,
                         "Air temperature (deg C)")
```

Now the for loop will look:
```python!
for num_measurements in [25, 100, 500]:
    temperatures = read_data("temperatures.csv",
                         num_measurements,
                         "Air temperature (deg C)")
    plot_temperatures(temperatures)
```

We are going to creat functions `create_name` and `save_plot`:
```python!
def create_name(num):
    name = f"plot_{str(num)}.png"
    return name

def save_plot(num):
    name = create_name(num)
    plt.savefig(name)
    plt.clf()
```

In order to make appear the plots in the saved file, we have to remove `plt.show()` in the function `plot_temperatures`.

The whole code then looks like:
```python=
import pandas as pd
from matplotlib import pyplot as plt


def compute_statistics(data):
    mean = sum(data)/ len(data)
    return mean

def read_data(filename, colname, num_measurements):
    data = pd.read_csv(filename, nrows=num_measurements)
    data_read = data[colname]
    return data_read


def plot_temperatures(temperatures):
    mean = compute_statistics(temperatures)

    # make labels
    plt.xlabel("measurements")
    plt.ylabel("air temperature (dec C)")

    # plot results
    plt.plot(temperatures, "r-")
    plt.axhline(y=mean, color="b", linestyle="--")
    plt.show()


for num_measurements in [25, 100, 500]:
    temperatures = read_data("temperatures.csv", "Air temperature (degC)", num_measurements)

    plot_temperatures(temperatures)
    save_plot(num_measurements)
```

We can still improve this code.
We are going to generalize `plot_temperatures` to `plot_data`:
```python!
def plot_data(data, mean, xlabel, ylabel, file_name):
    plt.plot(data, "r-")
    plt.xlabel(xlabel)
    plt.ylabel(ylabel)
    plt.axhline(y=mean, color="b", linestyle="--")
    plt.show()
    plt.savefig(file_name)
    plt.clf()
```

Then we actualize our for loop:
```python!
for num_measurements in [25, 100, 500]:

    temperatures = read_data(
        "temperatures.csv",
        "Air temperature (degC)",
        num_measurements
    )

    mean = compute_mean(temperatures)
    file_name = create_name(num_measurements)

    plot_data(
        data = temperatures,
        mean = mean,
        xlabel = "measurements",
        ylabel = "air temperature (deg C)",
        file_name = file_name,
    )
```

David's suggestion to improve our `plot_data` functioneed to change the `save_plot`:
```python!
def plot_data_differently(data, mean, xlabel, ylabel, file_name):
    fig, ax = plt.subplots()
    ax.plot(data, "r-")
    ax.axhline(y=mean, color="b", linestyle="--")
    ax.set_xlabel(xlabel)
    ax.set_ylabel(ylabel)
    return (fig, ax)

def save_plot(fig, num):
    name = create_name(num)
    fig.savefig(name)
    fig.clf()
```
In this case the for loop would be:
```python!
for num_measurements in [25, 100, 500]:

    temperatures = read_data(
        "temperatures.csv",
        "Air temperature (degC)",
        num_measurements
    )

    mean = compute_mean(temperatures)
    file_name = create_name(num_measurements)

    fig, ax =plot_data_differently(
        data = temperatures,
        mean = mean,
        xlabel = "measurements",
        ylabel = "air temperature (deg C)"
    )
    save_plot(fig, num_measurements)
```

Then the final script should look like:

```python!
import pandas as pd
from matplotlib import pyplot as plt


def compute_mean(data):
    mean = sum(data)/ len(data)
    return mean

def read_data(filename, colname, num_measurements):
    data = pd.read_csv(filename, nrows=num_measurements)
    data_read = data[colname]
    return data_read

def create_name(num):
    name = f"plot_{str(num)}.png"
    return name

def plot_data(data, mean, xlabel, ylabel):
    fig, ax = plt.subplots()
    ax.plot(data, "r-")
    ax.axhline(y=mean, color="b", linestyle="--")
    ax.set_xlabel(xlabel)
    ax.set_ylabel(ylabel)
    return(fig, ax)

def save_plot(fig, num):
    name = create_name(num)
    fig.savefig(name)
    fig.clf

for num_measurements in [25, 100, 500]:
    temperatures = read_data("temperatures.csv", "Air temperature (degC)", num_measurements)
    mean = compute_mean(temperatures)
    fig, ax = plot_data(data = temperatures,
                        mean = mean,
                        xlabel = "measurements",
                        ylabel = "air temperature (deg C)")
    save_plot(fig, num_measurements)


```
We are going to export the notebook to script: “File” -> “Save and Export Notebook As …” -> “Executable Script”.

In your teminal/git bash:
```bash!
git init
git add temperature_plotting.py
git commit -m "first working version"
git add temperatures.csv
git commit -m "add data"
```
#### comic relief
![](https://i.imgur.com/6c8lExX.jpg)


#### Code documentation
Write down what every thing is and does.
Target public (readers): future users / future us
Writting documentation in the beggining migh lead to lower development speed, but in the long run, in the future, your development speed will be lower.
Who are you writting the documentation for?: yourself? community?
*Sphinx:* tool for writting documentation

Documentation should be in your git repository. Updated code -> Updated docuemntation of the new features.

Open a new Jupyerlab notebook:
```bash=
conda activate coderefinery
jupyter-lab # Should open jupyter-lab in your browser
```

Let's take a look at two example comments (comments in python start with `#`):
#### Comment A
```python
# Now we check if temperature is larger than -50:
if temperature > -50:
    print('do something')
```

#### Comment B
```python
# We regard temperatures below -50 degrees as measurement errors
if temperature > -50:
    print('do something')
```


- 💀👻 *Zombie code:** Don't leave commented code (git is there for taking care of the history).

```python!
def mean_temperature(data):
    temperatures = data['Air temperature (deg C)']
    return sim(temperarures)/ len(temperatures)
```
In python theres is help command that shows an explanaiton of what a command or function does. In this example command `print`
```python!
help(print)
```
##### Creation of docstrings
For the function that we created we are going to create the doctrings follwoing google structure.
0. In Python: three double quotes `"""`
1. What does the function does
2. Args section: arguments of the function.
2.1 List arguments: name(type)
3. Returns section: description of what the function returns, add the type
4. Rasises section: Errors or exceptions that might arise during the excecution of the function
```python!
def mean_temperature(data):
    """
    Calculate mean temperature

    Args:
        data(pandas.DataFrame): A dataframe containing air temperature measurements

    Returns:
        The mean air temperature (float)

    """
    temperatures = data['Air temperature (deg C)']
    return sim(temperarures)/ len(temperatures)
```

Now you can run `help(mean_temperature)` and it will show the contents of the docstring.

##### README.md files

In [project](https://github.com/escience-academy/coderefinery-documentation-example-project) there is not a Readme file.
1. Fork the repository to your own account.
2. Put your Repository name.
3. You can clone it to your computer or make the changes in Github directly.
4. Select the option to create a `README.md file
5. You can add the code and you can click on preview to see how it is rendered.
```markdown!
### Temperature analysis in spreadsheets

A python script for the analysis of temperatures in excel files.

### Why should I use this project ?

It makes it easy to analyse excel files with temperatures in them.

### Setup -> What do you need to work with this project

You need `python>3.5` to run this script.

The project depends on the `pandas` library, install it with pip:
`pip install pandas`

### How to run?

You can run the script from the command-line using
`python analyse_spreadsheet.py`

### How to cite this project?

Please email `training@esciencecenter.nl` to get instructions on how to properly cite this project.

### Contributing
You are welcome to contribute to the code via pull requests.

```
6. Commit the changes.

Don't underestimate the power of a good README! It is the first thing (often) that people see when they encounter your project.

##### Documentation using Sphinx

Open a terminal and activate your conda environment and check that you have `sphinx-build` installed.
```bash=
conda activate coderefinery
sphinx-build --version # should print aphinx-build x.x.x
mkdir doc-example
cd doc-example
sphinx-quickstart
```
Then you will have to fill in some information type and then hit Enter.

This will create a bunch of files:
- index.rst : first page of your documentation, table of contents and index.
Add some content to index.rst:
*Note:* make sure that you are using correct indentation (3 spaces) and Enter space.
feature-a.md
and save the file.

`index.rst` should look like this:
```bash!
.. Example documentation project documentation master file, created by
   sphinx-quickstart on Wed Dec 14 12:23:18 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Example documentation project's documentation!
=========================================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:

   feature-a.md
```

Edit conf.py file:
```bash!
nano conf.py
```
add lines in #General section:
```bash!
extensions= ['myst_parser']
source_suffix = ['.rst', '.md']
```

Now we can modify feature-a.md
```bash=
# Some feature A

## Subsection

Some interesting documentation here.
Let's make a list:

- item 1

        - nested item 1
        - nested item 2

- item 2
- item 3
```

We are going to build our documentation. In your terminal:
```bash!
sphinx-build . _build # your documentation will be generated to the folder _build
# open the generated docs
open _build/ index.html # mac
start _build/ index.html # windows
```

In conf.py you can change the theme by modifying the line: `html_theme = 'sphinx_rtd_theme'`
This is a layout that lot's of projects use.


##### Deploy Sphinx documentation to GitHub Pages

Go to your repository on Github (or create one). [The example that Leon uses](https://github.com/loostrum/sphinx-doc-example)
Usually we store the documentaton in `doc` folder in your project.
Clone your repository.
Build the documentation, and open it.
Create a new folder `.github` and inside it another folder `workflows`:
```bash=
mkdir .github
cd .github
mkdir workflows
cd workflows
nano documentation.yaml
```
Create a new file at `.github/workflows/documentation.yaml` with the contents:

```yaml=
name: Docs
on: [push, pull_request, workflow_dispatch]
jobs:
  docs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
      - name: Install dependencies
        run: |
          pip install sphinx sphinx_rtd_theme
      - name: Sphinx build
        run: |
          sphinx-build doc _build
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: ${{ github.event_name == 'push' && github.ref == 'refs/heads/master' }}
        with:
          publish_branch: gh-pages
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: _build/
          force_orphan: true
```

Add it to Git:
```bash
git add documentation.yaml
git commit -m "add documentation workflow"

```

In github -> go to your repo -> three dots -> Settings -> Pages.
Enable Source -> Deploy from branch.

Push your repository:
```bash=
git push
```

The url where you should find your docuemntation is: `username.github.io/repository_name`

This is very nice because allows you to match documentation with the version of your code. Avoids having a miss-linked version of documentation.



## 📚 Resources
* [eScience Center call for proposals](https://www.esciencecenter.nl/calls-for-proposals/)
* [Upcoming workshops](https://www.esciencecenter.nl/digital-skills)
* [NL-RSE community](https://www.nl-rse.org)
*
* [Git commands cheat sheet](https://education.github.com/git-cheat-sheet-education.pdf)
* [Simple peer review real-life example](https://github.com/carpentries-incubator/deep-learning-intro/pull/269)
* [Show others how to cite your code with a CITATION.cff](https://citation-file-format.github.io/)
* [An example of an excellent README page](https://github.com/NLeSC/mcfly)
* [Another example of an excellent README page](https://github.com/amices/mice)