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
 * Adding a new target to the `Makefile`::

    github:
      @make html
      @cp -a build/html/. ./docs

 * Adding the matching `github` target to `make.bat` for Windows::

    :github
    %SPHINXBUILD% -M html %SOURCEDIR% %BUILDDIR% %SPHINXOPTS%
    if errorlevel 1 goto end
    xcopy /E /H /I /Y /Q "%BUILDDIR%\html" "docs"

To build HTML locally::

    $ make html

To build HTML and copy it into the `docs` folder for GitHub Pages::

    $ make github

On Windows, run the same targets with `make.bat`::

    > .\make html
    > .\make github

The GitHub Action itself runs `docs/buildsite.sh`, which builds the HTML static files and uses the GitHub Actions environment variables including the Secrets storage.

> Note: When the personal access token format changed, I had to update the Secret in the GitHub Actions settings so that the build would work again.
