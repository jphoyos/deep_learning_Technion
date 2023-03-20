---
title: Getting started with the course assignments
permalink: assignments/getting-started
toc: true
toc_label: Contents
toc_sticky: true
date: 2022-03-23
copyright:
  name: aviv
  icon: fas fa-at
published: true
---

This document will help you get started with the course homework assignments.
Please read it carefully as it contains crucial information.

## General

The course homework assignments are mandatory and a large part of the grade.
They entail writing code in python using popular third-party machine-learning
libraries and also theoretical questions.

The assignments are implemented in part on a platform called Jupyter notebooks.
[Jupyter](http://jupyter.org/) is a widely-used tool in the machine-learning
ecosystem which allows us to create interactive notebooks containing live code,
equations and text. We'll use jupyter notebooks to guide you through the
assignments, explain concepts, test your solutions and visualize their outputs.

To install and manage all the necessary packages and dependencies for the
assignments, we use [conda](https://conda.io), a popular package-manager for
python.  The homework assignments come with an `environment.yml` file which
defines what third-party libraries we depend on. Conda will use this file to
create a virtual environment for you. This virtual environment includes python
and all other packages and tools we specified, separated from any preexisting
python installation you may have. Detailed installation instructions are below.
We will not support any other installation method other than the one
described.

For working on the code itself, we recommend using
[PyCharm](https://www.jetbrains.com/pycharm/), however you can use any other
editor or IDE if you prefer. You can obtain the professional version of PyCharm
for free by using your Technion student email (see
[here](https://www.jetbrains.com/student/)).

### Project structure

Each assignment's root directory contains the following files and folders:

- `cs236781`: Python package containing course utilities and helper functions.
  You do not need to edit anything here.
- `hwN` where `N` is the assignment number: Python package containing the
  assignment code. **All** your solutions will be implemented here, including
  answers to questions.
- `PartN_XYZ.ipynb` where `N` is a number and `XYZ` is some name:
  A set of jupyter notebooks that contain the instructions that will guide you
  through the assignment. You do **not** need to edit these. However, you
  should write your name(s) at the beginning of `Part0`.
- `main.py`: A script providing some utilities via a CLI.
  You'll run it to create your submission after completing the
  assignment.
- `environment.yml`: A file for `conda`, specifying the third-party packages it
  should install into the virtual environment it creates. Note that every
  assignment could define a different environment.

## Environment set-up

1. Install the python3 version of [miniconda](https://conda.io/miniconda.html).
   Follow the [installation instructions](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html)
   for your platform.

   For example, on linux you should do:

    ```shell
    curl -fsSLO https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
    bash Miniconda3-latest-Linux-x86_64.sh
    # Accept EULA
    # Install in default directory
    # Select yes for running conda init
    ```

   On macOS it's similar but with a different script URL

    ```shell
    curl -fsSLO https://repo.continuum.io/miniconda/Miniconda3-latest-MacOSX-x86_64.sh 
    bash Miniconda3-latest-MacOSX-x86_64.sh
    # Rest is the same
    ```

   On Windows, download the installer and follow the instructions on the conda
   website. See also the Windows-specific notes below before you proceed.

   Note that you can skip this step if you already have either `conda` or the
   full Anaconda distribution installed.

2. Recommended: configure `conda` to use strict channel priority (will speed up solving the
   environment) and to not automatically activate the default env (will force
   you to activate a specific env):
    ```shell
    conda config --set channel_priority strict
    conda config --set auto_activate_base False
    ```

3. Install [mamba](https://github.com/mamba-org/mamba) (a drop-in replacement
   for `conda` which is much faster in solving the dependency requirements):
    ```shell
    conda install -n base -c conda-forge mamba
    mamba init
    ```

4. Use `mamba` to create a virtual environment for the assignment.
   From the assignment's root directory, run

    ```shell
    mamba env update -f environment.yml -n cs236781-hw
    ```
   This will install all the necessary packages into a new virtual
   environment named `cs236781-hw`.

   From here on you can use either `conda` or `mamba` (they have exactly the same
   CLI), but for this course generally `mamba` will be much faster. You can
   even `alias conda=mamba`.

   Note for users with M1 macs (Apple Silicon): You'll need to install the
   Intel versions of the packages (they'll run fine via rosetta2).
   To do this, run `export CONDA_SUBDIR=osx-64` before running the above
   `mamba` command.

5. Activate the new environment by running e.g.

    ```shell
    conda activate cs236781-hw
    ```

   Note: *Activating* an environment simply means that the path to its python binaries
   (and packages) is placed at the beginning of your `$PATH` shell variable.
   Therefore, running programs installed into the conda env (e.g. `python`) will
   run the version from the env since it appears in the `$PATH` before any other
   installed version.

   To check what conda environments you have and which is active, run

    ```shell
    conda env list
    ```

   or, you can run `which python` and you should see the python binary is in a
   subfolder of e.g. `~/miniconda3/envs/cs236781-hw/`.

   You can find more useful info about conda environments
   [here](https://conda.io/docs/user-guide/tasks/manage-environments.html).

### General Notes

- You should to do steps 1 (installing `conda`) once, not for each assignment.

- However, the third-party package dependencies (in the `environment.yml` file)
  might slightly change from one assignment to the next, or in case an update
  is published.
  To make sure you have the correct versions, always install the environment
  again (**step 4 above**) from the assignment root directory every time a new
  assignment is published and then activate the environment with the assignment
  number.

- Always make sure the correct environment is active! Each time you close and
  re-open your terminal, the environment will need to be activated again.

- If you use PyCharm or any other IDE, you should configure the interpreter path
  of the IDE to the path of the `python` executable within the conda
  env folder. For example, point the interpreter path to
  `~/miniconda3/envs/cs236781-hw/bin/python`.
  This is under `Settings -> Project -> Project Interpreter`.

- You'll need to install the conda env within your user folder on the course
  server. The installation procedure is exactly the same, just follow the
  instructions for linux.

### Notes for Windows Users

- On Windows, you can run these commands from the **Anaconda Prompt** program
  that is installed with miniconda. If you also add the `conda` installation
  to the Windows `PATH` variable, you can run these commands from the regular
  windows command prompt.

- Also on Windows, you may need to install Microsoft's [Build Tools for Visual
  Studio](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019)
  before the conda environment.  Make sure "C++ Build Tools" is selected during
  installation. This only needs to be done once.

## Working on the assignment

### Running Jupyter

Make sure that the active conda environment is `cs236781-hw` (see above), and
run

```shell
jupyter lab
```

This will start a [jupyter lab](https://jupyterlab.readthedocs.io/en/stable/)
server and open your browser at the local server's url. You can now start working.
Open the first notebook (`Part0`) and follow the instructions.

If you're new to jupyter notebooks, you can get started by reading the
[UI guide](https://jupyter-notebook.readthedocs.io/en/stable/notebook.html#notebook-user-interface)
and also about how to use notebooks in
[JupyterLab](https://jupyterlab.readthedocs.io/en/latest/user/notebook.html).

Note that if you are familiar with and prefer the regular `jupyter notebook` you
can use that instead of `jupyter lab`.

### Implementing your solution and answering questions

- The assignment is comprised of a set of notebooks and accompanying code
  packages.
- You only need to edit files in the code package corresponding to the
  assignment number, e.g. `hw1`, `hw2`, etc.
- The notebooks contain material you need to know, instructions about what to do
  and also code blocks that will **test and visualize** your implementations.
- Within the notebooks, anything you need to do is marked with a **TODO** beside
  it. It will explain what to implement and in which file.
- Within the assignment code package, all locations where you need to write code
  are marked with a special marker (`YOUR CODE`). Additionally, implementation
  guidelines, technical details and hints are in some cases provided in a
  comment above.
- Sometimes there are open questions to answer. Your answers should also be
  written within the assignment package, not within the notebook itself. The
  notebook will specify where to write each answer.

Notes:

1. You should think of the code blocks in the notebooks as tests. They test your
   solutions and they will fail if something is wrong.  As such, if you
   implement everything and the notebook runs without error, you can be
   confident about your solution.

2. You **may** edit any part of the code, not just the sections marked with
   `YOUR CODE`. However, note that there is always a solution which requires
   editing only within these markers.

3. When we check your submission, we'll run the **original notebook files** of
   the assignment, together with your submitted code (from the `hwN`) package.
   Therefore, any changes you do to the notebook files (such as changing the
   tests) will not affect the results of our grading. If you rely on notebook
   modifications to pass the tests, the tests will fail when we grade your work
   and you will lose marks.

4. Please don't put other files in the assignment directory. If you do, they
   will be added to your submission which is automatically generated from the
   contents of the assignment folder.

5. Always make sure the active conda env is `cs236781-hw`. If you get strange
   errors or failing import statements, this is probably the reason. Note that
   if you close your terminal session you will need to re-activate since conda
   will use it's default `base` environment.

## Submitting the assignment

What you'll submit:
- All notebooks, after running them clean from start to end, with all outputs
  present.
- An html file containing the merged content of all notebooks.
- The code package (`hwN`), with all your solutions present.

You don't need to do this manually; we provide you with a helper CLI program to
run all the notebooks and combine them into a single file for submission.

### Generating your submission file

To generate your submission, run (obviously with different id's):

```shell
python main.py prepare-submission --id 123456789 --id 987654321
```

The above command will:
- Execute all the notebooks cleanly, from start to end, regenerating all outputs.
- Merge the notebook contents into a single html file.
- Create a zip file with all of the above and also with your code.

If there are errors when running your notebooks, it means there's a problem with
your solution or that you forgot to implement something.

Additionally, you can use the `--skip-run` flag to skip running your notebooks
(and just merge them) in case you already ran everything and you're sure that
all outputs are present:

```shell
python main.py prepare-submission --skip-run --id 123456789 --id 987654321
```

Note however that if some of the outputs are missing from your submission you'll
lose marks.

**Note**: The submission script must also be run from within the same `conda env` as
the assignment. Don't forget to activate the env before running the submission
script!

### Submitting a partial solution

If you are unable to solve the entire assignment and wish to submit a partial
solution you can create a submission with errors by adding an `allow-errors`
flag, like so:

```shell
python main.py prepare-submission --allow-errors --id 123456789 --id 987654321
```

### Uploading the solution

The `.zip` file you generate should be uploaded using the assignments tab in the
[webcourse](https://webcourse.cs.technion.ac.il/236781/) system.

Grades will also be reported there.

Only a submission generated by the course script is considered valid. Any
other submissions, e.g. submitting only the notebooks or the code files will
**not be graded**.
