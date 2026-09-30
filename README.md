# python-repos-template

A [copier](https://copier.readthedocs.io/) template for small Python projects:
[uv](https://docs.astral.sh/uv/) for packaging,
[ruff](https://docs.astral.sh/ruff/) for linting and formatting,
[pre-commit](https://pre-commit.com/) to keep the repo clean, and a `notebooks/`
folder.

## Create a project

```bash
uvx copier copy --trust gh:tchauffi/python-repos-template my-project
```

Copier asks for the project name (defaults to the folder name), a description,
the author name and email, the Python version, and whether to create a GitHub
repository. Then it:

1. renders the project with your names filled in,
2. runs `git init`, `uv sync` and `pre-commit install`,
3. makes the initial commit,
4. optionally runs `gh repo create --source . --push`.

`--trust` is required because the template runs those setup commands.

### Skip typing your name and email

Copier reads default answers from a user settings file
(`~/Library/Application Support/copier/settings.yml` on macOS,
`~/.config/copier/settings.yml` on Linux):

```yaml
defaults:
  author_name: Your Name
  author_email: you@example.com
```

## Update an existing project

From inside a generated project:

```bash
uvx copier update --trust
```

Copier re-applies the template and merges your changes with the new version.

## What you get

```text
my-project/
├── .github/workflows/ci.yml   # pre-commit + pytest on pushes and PRs
├── notebooks/example.ipynb
├── src/my_project/__init__.py
├── tests/test_main.py         # pytest example
├── .copier-answers.yml        # used by `copier update`
├── .gitignore
├── .pre-commit-config.yaml    # hygiene checks, ruff, nbstripout, uv-lock
├── .python-version
├── Makefile                   # make setup / test / lint / format / update / clean
├── pyproject.toml
├── README.md
└── uv.lock
```

## Developing the template

The template lives in `template/`; questions and setup tasks are in
`copier.yml`. To try local changes:

```bash
uvx copier copy --trust --vcs-ref HEAD . /tmp/demo-project
```

CI renders the template with default answers and runs the generated project's
hooks and tests on every push.
