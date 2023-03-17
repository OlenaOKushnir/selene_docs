# OUTDATED and DEPRECATED selene docs source

This repository contains files with docs source for selene (initially created in 2017).

Now it serves as place for adding redirection to new Selene website:

[New Selene documentation website](https://yashaka.github.io/selene/)

_(since March, 2023)_

## Note for maintainers

For local docs preview (local build):

1. Clone this repo
2. In project root directory, execute:

    `poetry install`

3. Activate Python virtual environment. The easiest way is:

    `poetry shell`

4. Build HTML pages to `./build/html` folder:

    `make html`

### Correlation Table

The following table helps to recall, which old RTD site is built from (what branch).

❗ DO NOT MERGE THESE BRANCHES WITH MASTER ❗  
_(or vice versa)_

| Branch | RTD project | Website |
|--------|--------|--------|
| `master`| https://readthedocs.org/projects/selene-docs-test/| [selene-docs-test.readthedocs.io](https://selene-docs-test.readthedocs.io/) <br><br>|
| `rtd-selene-documentation-domain`| https://readthedocs.org/projects/selene-documentation/ <br><br> https://readthedocs.org/projects/selene-docs/| [selene-documentation.readthedocs.io](https://selene-documentation.readthedocs.io/) <br><br><br> [selene-docs.readthedocs.io](http://selene-docs.readthedocs.io/)<br><br>|
| `???` <br> ❗ NO ACCESS to this RTD project | https://readthedocs.org/projects/selene/<br><br><br>| [selene.readthedocs.io](https://selene.readthedocs.io/) <br> _(version (content) is the same as above branch and it can be used as source branch)_|

**Note:** Different branches are created intentionally. Because websites were configured with two different Sphinx themes: `agogo` and `alabaster` (in 2017). In order not to shock users too much _(auto redirect is enough for that)_ these themes were preserved. After several years (when ALL old websites disappear from Google search), maintainers can leave one of the branch for all old websites (changing default / source branch in RTD project admin panel).
