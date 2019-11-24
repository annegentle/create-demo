Welcome to the Create Demo project
==================================

This repo shows an example of how to use GitHub Pages with Python Sphinx builds.

There are some pre-requisites to building locally:

  * Python installed
  * Sphinx installed (best in a virtual environment)

The magic parts for GitHub Pages builds are:

 * Having the docs source files in a /docs folder.
 * Adding an empty `.nojekyll` file in the root of the /docs folder.
 * Adding a new target to the `Makefile` and `make.bat` file::

    github:
      @make html
      @cp -a _build/html/. ./docs

To build HTML locally::
    $ make html

To build for GitHub::
    $ make github
