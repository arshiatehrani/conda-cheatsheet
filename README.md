# Conda Commands and Environment Management

Here's a comprehensive guide to Conda environment management, including essential commands, comparisons with Pip, and channel configuration.

-----

## Basic Conda Commands

| Task | Command | Example |
| :-- | :-- | :-- |
| Check conda version | `conda --version` | `conda --version` |
| Get help for a command | `conda <cmd> --help` | `conda create --help` |
| Show conda info | `conda info` | `conda info` |

-----

## Create Environments

| Task | Command | Example |
| :-- | :-- | :-- |
| Create empty env (no packages) | `conda create -n <name>` | `conda create -n myenv` |
| Create with latest Python | `conda create -n <name> python` | `conda create -n myenv python` |
| Create with specific Python | `conda create -n <name> python=<ver>` | `conda create -n py311 python=3.11` |
| Create with Python and packages | `conda create -n <name> python=<ver> <pkg> ...` | `conda create -n ds python=3.10 numpy pandas jupyter` |
| Create with specific package versions | `conda create -n <name> <pkg>=<ver> ...` | `conda create -n sci scipy=1.11 matplotlib=3.8` |
| Create from YAML | `conda env create -f environment.yml` | `conda env create -f environment.yml` |
| Create at custom path (prefix) | `conda create --prefix <path> ...` | `conda create --prefix ./envs/proj python=3.11` |
| Create targeting a platform (advanced) | `conda create --platform <subdir> -n <name> ...` | `conda create --platform osx-64 -n pyx64 python` |

-----

## Activate / Deactivate Environments

| Task | Command | Example |
| :-- | :-- | :-- |
| Activate by name | `conda activate <name>` | `conda activate myenv` |
| Activate by path (prefix) | `conda activate <path>` | `conda activate ./envs/proj` |
| Deactivate current env | `conda deactivate` | `conda deactivate` |

-----

## List Environments and Packages

| Task | Command | Example |
| :-- | :-- | :-- |
| List environments | `conda env list` | `conda env list` |
| List packages in current env | `conda list` | `conda list` |
| List packages in a named env | `conda list -n <name>` | `conda list -n myenv` |
| Show envs via info | `conda info --envs` | `conda info --envs` |

-----

## Install, Update, Remove Packages

| Task | Command | Example |
| :-- | :-- | :-- |
| Install package in active env | `conda install <pkg>` | `conda install seaborn` |
| Install into named env | `conda install -n <name> <pkg>` | `conda install -n ds scikit-learn` |
| Install specific version | `conda install <pkg>=<ver>` | `conda install numpy=1.26` |
| Install from channel | `conda install -c <channel> <pkg>` | `conda install -c conda-forge xgboost` |
| Update a package | `conda update <pkg>` | `conda update pandas` |
| Update all packages | `conda update --all` | `conda update --all` |
| Remove a package | `conda remove <pkg>` | `conda remove matplotlib` |
| Search for packages | `conda search <pattern>` | `conda search pytorch` |

-----

## Remove, Clone, Export Environments

| Task | Command | Example |
| :-- | :-- | :-- |
| Remove env by name | `conda remove -n <name> --all` | `conda remove -n myenv --all` |
| Remove env (env subcommand) | `conda env remove -n <name>` | `conda env remove -n myenv` |
| Remove env by path | `conda remove --prefix <path> --all` | `conda remove --prefix ./envs/proj --all` |
| Clone environment | `conda create --clone <src> -n <dest>` | `conda create --clone ds -n ds-copy` |
| Export exact spec (cross-OS YAML) | `conda env export -n <name> > environment.yml` | `conda env export -n ds > environment.yml` |
| Export explicit lockfile | `conda list --explicit > pkgs.txt` | `conda list --explicit > pkgs.txt` |
| Create from explicit file | `conda create -n <name> --file pkgs.txt` | `conda create -n exact --file pkgs.txt` |

-----

## Revisions and Rollback

| Task | Command | Example |
| :-- | :-- | :-- |
| List history (current env) | `conda list --revisions` | `conda list --revisions` |
| Roll back to a revision | `conda install --revision <num>` | `conda install --revision 3` |
| List history (named env) | `conda list -n <name> --revisions` | `conda list -n ds --revisions` |

-----

## Quality-of-Life Flags

| Use case | Flag | Example |
| :-- | :-- | :-- |
| Auto-confirm actions | `-y` | `conda create -n ds python=3.10 -y` |
| Create without default packages | `--no-default-packages` | `conda create -n clean python --no-default-packages` |
| Specify channels inline | `-c <channel>` | `conda install -c conda-forge mamba` |

-----

## Minimal End-to-End Examples

  - **Simple env with latest Python:**
      - `conda create -n simple python -y`
      - `conda activate simple`
  - **Env with Python 3.11 and key packages:**
      - `conda create -n ml python=3.11 numpy pandas scikit-learn jupyter -y`
      - `conda activate ml`
  - **Create from environment.yml:**
      - `conda env create -f environment.yml`
      - `conda activate <name_from_yml>`
  - **Export and recreate:**
      - `conda env export -n ml > environment.yml`
      - `conda env remove -n ml`
      - `conda env create -f environment.yml`
  - **Delete an environment:**
      - `conda remove -n simple --all`

**Tip:** Install as many needed packages as possible at creation time to reduce dependency conflicts.

-----

## Conda vs. Pip — Super Simple Comparison

  - **Conda**: Manages **environments** and installs **any kind of package** (Python, R, C, system libraries, etc.). Good for data science and complex setups. Can install Python itself.
  - **Pip**: Installs **Python packages only** (from PyPI). Needs Python already installed. Use with `venv` or `virtualenv` for isolation.

| Tool | What it installs | Manages environments? | Typical use case |
| :-- | :-- | :-- | :-- |
| Conda | Any software (not just Python) | Yes | Data science, mixed stacks |
| Pip | Python packages only | No (needs venv) | Pure Python projects |

**If you want to install more than just Python stuff, or need easy environment management, use Conda. If you just need Python packages, Pip is enough.**

-----

## Super Simple Guideline: `pip install` vs `conda install`

| Command | What it installs | Where it works | Handles non-Python stuff? | Manages environments? |
| :-- | :-- | :-- | :-- | :-- |
| `pip install` | **Python packages only** | Any Python environment | **No** | **No** (use venv) |
| `conda install` | **Any package** (Python, R, C, etc.) | Only in conda envs | **Yes** | **Yes** |

**Quick rule:**

  - Use `pip install` for pure Python projects.
  - Use `conda install` for data science, scientific computing, or if you need non-Python stuff (like C libraries, R, etc.).

**If you use Conda environments, prefer `conda install` first. If a package isn't available, use `pip install` inside the Conda env.**

-----

## Add conda-forge Channel and Set Priority

### Add conda-forge as highest priority channel:

```bash
conda config --add channels conda-forge
```

### Set strict channel priority:

```bash
conda config --set channel_priority strict
```

### (Optional) Show your channel list:

```bash
conda config --show channels
```

### (Optional) Install a package from conda-forge (one-time, without adding channel):

```bash
conda install -c conda-forge <package>
```

**Summary:**

  - Use `--add` to put `conda-forge` at the top (highest priority).
  - Use `--set channel_priority strict` to make Conda always prefer higher-priority channels.
  - After this, you can just use `conda install <package>` and it will find packages from `conda-forge` automatically.

-----

## Export a Conda Environment to `environment.yml`

To export an active Conda environment (e.g., named "p") to an `environment.yml` file, use the following commands:

  - **On Windows (PowerShell):**
    ```powershell
    conda activate p; conda env export > environment.yml
    ```
  - **On macOS/Linux (bash/zsh):**
    ```bash
    conda activate p && conda env export > environment.yml
    ```

**Tip:** For a cross-platform, minimal specification that only includes explicitly installed packages, use:

```bash
conda activate p && conda env export --from-history > environment.yml
```
