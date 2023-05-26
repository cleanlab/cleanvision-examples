# Development

This guide provides a checklist for contributing new cleanvision examples.

- Ensure that the notebook contains cell outputs and that they look as expected in Jupyter notebook and **on GitHub**.
  Note this is different than our tutorials in the main cleanlab repository (where notebook cells should not be
  executed)! Unlike the tutorials, we want examples notebooks to also look good in GitHub's viewer (which has limited
  rendering functionality, so avoid things like `<div>` that GitHub's viewer does not render properly).

- Ensure that the jupyter notebook cells are executed in order. Additionally clear any cell blocks that are too large (
  eg. model training code that specifies accuracy for each epoch), it is ok if these do not have an execution number
  after being cleared.

- The first cell of the notebook should be a markdown block containing the text:
    ```
    [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/cleanlab/cleanvision-examples/blob/main/{ relative path to notebook }.ipynb)
    ``` 

  Replace the `{ relative path to notebook }` portion with the path to the notebook relative to the root folder.

  > eg. the [caltech256.ipynb](caltech256.ipynb) notebook will have a relative path of `caltech256.ipynb` and will have
  the badge:
  >
  > ```
    > [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/cleanlab/cleanvision-examples/blob/main/caltech256.ipynb)
    > ```

  This will create a badge that will link to a Google Colab version of the notebook.

  Note that the Colab badge links to the notebook in the main branch, so at the time of making the PR, the link will be
  invalid. Please remember to check that the Colab link works after the PR has been approved and merged to `main`.

  The Colab badge must also be in its own notebook cell, not with other content.

- Ensure that your notebook is using the correct kernel. In jupyter notebook, you can check the notebook's metadata by
  navigating to `Edit` > `Edit Notebook Metadata` and check if the follow fields match this:

```json
"kernelspec": {
"name": "python3",
"display_name": "Python 3 (ipykernel)",
"language": "python"
}
```

- Add the notebook to the [README](README.md), ideally grouping the newly added example with any other related examples.

- After a new notebook has been added and pushed to `main` branch, AVOID changing the notebook and folder names, as this
  may break existing links referencing the example notebook throughout cleanvision documentation, blog posts, and more.

- If the example requires some packages other than the ones in [requirements-dev.txt](requirements-dev.txt), Please
  create a separate `requirements.txt` specific to that example with extra packages required. Put these requirements and
  any related jupyter notebooks in a directory instead of the root folder.

## Set up the environment for running notebooks

While this is not required, we recommend that you do development and testing in a virtual environment. There are a
number of tools to do this, including [virtualenv](https://virtualenv.pypa.io/), [pipenv](https://pipenv.pypa.io/),
and [venv](https://docs.python.org/3/library/venv.html). You
can [compare](https://stackoverflow.com/questions/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe)
the tools and choose what is right for you. Here, we'll explain how to get set up with venv, which is built in to Python

```shell
python3 -m venv cleanvision-examples  # create a new virtual environment in the directory ENV
source cleanvision-examples/bin/activate  # switch to using the virtual environment
pip install --upgrade pip
pip install -r requirements-dev.txt
python -m ipykernel install --user --name=cleanvision-examples
```

Choose the `cleanvision-examples` kernel in the jupyter notebook when running.

You only need to create the virtual environment once, but you will need to
activate it every time you start a new shell. Once the virtual environment is
activated, the `pip install` commands below will install dependencies into the
virtual environment rather than your system Python installation.
