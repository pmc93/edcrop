# Installation and Quickstart
## Installation

Edcrop (v. 1.0.0) is coded in and requires Python 3.8.8 or higher. It uses the packages numpy (v. 1.20.1),
pandas (v. 1.2.4), matplotlib (v. 3.3.4), and yaml (pyyaml v. 5.4.1).

Edcrop is available from the Python Package Index (PyPI.org) repository. It is installed by executing from the
command line

emsp **pip install edcrop**

> This installation uses the following dependencies of other Python packages:
> dependencies = [
> "numpy >=1.20.1",
> "matplotlib >= 3.3.4",
> "pandas >=1.2.4",
> "pyyaml >=5.4.1"]

To install Edcrop without caring for dependencies, use instead
**pip install --no-deps edcrop**
The above commands install Edcrop into the Python site-packages directory. The edcrop directory contains
a sub-directory named Examples, containing example of data files required to make Edcrop run.
To learn more about installation by use of pip (the package installer for Python), consult the pip
documentation, e.g. https://pip.pypa.io/en/stable/cli/pip_install/.
Edcrop and example releases can also be found on https://github.com/SteenChr/edcrop.

## What is MyST?

MyST stands for "Markedly Structured Text". It
is a slight variation on a flavor of markdown called "CommonMark" markdown,
with small syntax extensions to allow you to write **roles** and **directives**
in the Sphinx ecosystem.

For more about MyST, see [the MyST Markdown Overview](https://jupyterbook.org/content/myst.html).

## Sample Roles and Directives

Roles and directives are two of the most powerful tools in Jupyter Book. They
are kind of like functions, but written in a markup language. They both
serve a similar purpose, but **roles are written in one line**, whereas
**directives span many lines**. They both accept different kinds of inputs,
and what they do with those inputs depends on the specific role or directive
that is being called.

Here is a "note" directive:

```{note}
Here is a note
```

It will be rendered in a special box when you build your book.

Here is an inline directive to refer to a document: {doc}`markdown-notebooks`.


## Citations

You can also cite references that are stored in a `bibtex` file. For example,
the following syntax: `` {cite}`holdgraf_evidence_2014` `` will render like
this: {cite}`holdgraf_evidence_2014`.

Moreover, you can insert a bibliography into your page with this syntax:
The `{bibliography}` directive must be used for all the `{cite}` roles to
render properly.
For example, if the references for your book are stored in `references.bib`,
then the bibliography is inserted with:

```{bibliography}
```

## Learn more

This is just a simple starter to get you started.
You can learn a lot more at [jupyterbook.org](https://jupyterbook.org).
