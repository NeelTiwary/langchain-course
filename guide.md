# Starting a Python project with uv

This guide covers installing `uv`, initializing a project, managing dependencies, and running code on Windows.

## 1. Install uv

In PowerShell, install `uv` with WinGet:

```powershell
winget install --id astral-sh.uv -e
```

Open a new PowerShell window and verify the installation:

```powershell
uv --version
```

## 2. Initialize a project

From the folder where you keep your projects, create a project using Python 3.11:

```powershell
uv init --python 3.11 my-project
cd my-project
```

`uv init` creates the project files, including `pyproject.toml` and a starter Python file. It does not need a manually created virtual environment.

## 3. Add dependencies

Add runtime dependencies with `uv add`. For example:

```powershell
uv add langchain
```

Add development tools as development dependencies:

```powershell
uv add --dev pytest ruff
```

`uv` records dependencies in `pyproject.toml` and updates `uv.lock`.

## 4. Sync and run the project

Install the project's dependencies and create its local `.venv` if it does not already exist:

```powershell
uv sync
```

Run Python through `uv` so it uses the project's environment:

```powershell
uv run python main.py
```

For a script or command declared in `pyproject.toml`, use `uv run` with that command. For example, this project declares `langchain-course`:

```powershell
uv run langchain-course
```

You can also activate the environment manually in PowerShell when needed:

```powershell
.\.venv\Scripts\Activate.ps1
```

Leave it with:

```powershell
deactivate
```

Activation is optional; `uv run` is usually simpler.

## 5. Work with an existing project

For an existing project that already has `pyproject.toml` and `uv.lock`, go to that folder and run:

```powershell
uv sync
uv run python main.py
```

In this repository, the LangChain project is in `langchain-course` and already has a local `.venv`. Run `uv sync` from that folder to synchronize it with the lockfile; there is no need to use the workspace-level `venv`.

## 6. Keep in source control

- Commit `pyproject.toml` and `uv.lock` for reproducible installs.
- Do not commit `.venv` or `.env`. Keep API keys in `.env`, and load them from application code.
- To pin a project's Python version, run `uv python pin 3.11`; this writes the `.python-version` file.

Useful commands:

```powershell
uv add package-name
uv remove package-name
uv add --dev package-name
uv sync
uv run <command>
uv lock
```
