Welcome to the Create Demo project
==================================

This repo shows an example of how to use GitHub Pages with Python Sphinx builds.

There are some pre-requisites to building locally:

  * [Python installed](https://docs.python-guide.org/starting/installation/)
  * [Sphinx installed](https://www.sphinx-doc.org/en/master/usage/installation.html) (best in a [virtual environment](https://docs.python.org/3/library/venv.html))

If you see errors like `Makefile:17: *** missing separator.  Stop.`, likely you do not have [Sphinx installed](https://www.sphinx-doc.org/en/master/usage/installation.html) locally.

The magic parts for GitHub Pages builds are:

 * Having the docs source files in a /docs folder.
 * Adding an empty `.nojekyll` file in the root of the /docs folder.
 * Having a script that builds the static files for the GitHub Action to run. 
 * Adding a new target to the `Makefile` and `make.bat` file::

    github:
      @make html
      @cp -a _build/html/. ./docs

To build HTML locally::
    $ make html

The build for GitHub is only used by the GitHub Action. It which makes the HTML static files and uses the GitHub Actions environment variables including the Secrets storage. 
    `$ make github`
