## Cookiecutter UBC-MDS

**Cookiecutter** template for a UBC-MDS Python packge.
-  Free software: BSD license

### Features

-  **pytest** testing: Setup to easily test for Python 3.7 & 3.8 (other Python versions can be added by editing the GitHub Actions workflow file) across ubuntu, mac and windows operating systems
-  **GitHub Actions**: Ready for GitHub Actions Continuous Integration testing & Deployment
-  **codecov**: Code coverage report and badge using codecov and GitHub Actions
-  **Sphinx** docs: Documentation ready for generation with, for
   example, **ReadTheDocs**
-  **Python-semantic-release**: Pre-configured version bumping upon merging pull request to master
-  Auto-release to **testPyPI** upon merging pull request to master

### Quickstart

1. Install the latest Cookiecutter if you haven't installed it yet (this
requires Cookiecutter 1.4.0 or higher)

   ```
   pip install -U cookiecutter
   ```

2. Generate a Python package file and directory structure:
   ```
   cookiecutter https://github.com/UBC-MDS/cookiecutter-ubc-mds.git
   ```

3. Initialize it with Poetry. Responding no to the ask of interactively installing dependencies or development dependencies.
   ```
   cd <your_project>
   poetry init
   ```
   
4. Install the required development dependencies:
   ``` 
   poetry add --dev pytest pytest-cov codecov python-semantic-release flake8 sphinx sphinxcontrib-napoleon
   ```
  
5. Create a remote version control repository on GitHub for this project, and link it to <https://codecov.io/>. Get the repository token from <https://codecov.io/> and record is as a secret on GitHub using the name `CODECOV_TOKEN`.
    
6. Write the code and tests for your Python package! And use Python poetry to install, add dependencies and test your package locally. For more details, see the [py-pkgs book](https://ubc-mds.github.io/py-pkgs/).

7. Render your documentation:
   ```
   poetry run sphinx-apidoc -f -o docs/source <your_project>
   cd docs
   poetry run make html
   ```

8. Put your local files under version control with Git, add the GitHub repository you set up as the remote and push your changes to GitHub! 

9. To have your docs appear on Read the Docs, follow the instructions here: <https://dont-be-afraid-to-commit.readthedocs.io/en/latest/documentation.html#readthedocs-org>

10. Add the following information to the `[tool.poetry]` table in `pyproject.toml`:
   ```
   readme = "README.md"
   homepage = "https://github.com/<github_username>/<github_repo>"
   repository = "https://github.com/<github_username>/<github_repo>"
   documentation = 'https://<package_name>.readthedocs.io'
   ```

11. When you are satisfied, use poetry to publish your package to testPyPI.


#### Optional (automated version bumping and release to test PyPI)

12. Add the following to the `pyproject.toml` file (substituting <your_project> with the appropriate value):
   ```
   [tool.semantic_release]
   version_variable = "<your_project>/__init__.py:__version__"
   version_source = "commit"
   upload_to_pypi = "false"
   patch_without_tag = "true"
   ```

13. Add the following secrets to the project's repository on GitHub:
   - TEST_PYPI_USERNAME
   - TEST_PYPI_PASSWORD

14. Put your local files under version control with Git, add the GitHub repository you set up as the remote and push your changes to GitHub and Let the magic happen!

For more details, see the [py-pkgs book](https://ubc-mds.github.io/py-pkgs/).

#### Optional (push to PyPI as opposed to testPyPI)

15. Once you are happy with the state of your package, and you want to publish to PyPI as opposed to testPyPI, all you need to do is add your PYPI_USERNAME & PYPI_PASSWORD to your project repo as GitHub secrets and change [this line](https://github.com/UBC-MDS/cookiecutter-ubc-mds/blob/bd8cb34f83d6341c411954322354031602606b80/%7B%7Bcookiecutter.project_slug%7D%7D/.github/workflows/release.yml#L80) of the release GitHub Actions workflow to this:

```
poetry publish -u $PYPI_USERNAME -p $PYPI_PASSWORD
```

### Credits

This template was modified from the [pyOpenSci/cookiecutter-pyopensci](https://github.com/pyOpenSci/cookiecutter-pyopensci) project template and the [audreyr/cookiecutter-pypackage](https://github.com/audreyr/cookiecutter-pypackage).
