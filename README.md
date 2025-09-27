# conda-cheatsheet
Conda Cheat Sheet — Environments &amp; Packages
Perfect 👍 I’ll integrate your new content into the README under a dedicated section called **“Exporting an Environment to YAML”**, right after the **Remove, Clone, Export Environments** section (since it fits naturally there).

Here’s the updated **README.md**:

---

````markdown
# 📘 Conda Cheat Sheet — Environments & Packages

<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" alt="conda logo" height="64" />

A clear and practical reference for common **conda environment and package management commands**.  
This cheat sheet helps you create, manage, clone, and delete environments, install packages, and compare `conda` vs `pip`.

---

## 🔹 Basics

| Task | Command | Example |
| :-- | :-- | :-- |
| Check conda version | `conda --version` | `conda --version` |
| Get help for a command | `conda <cmd> --help` | `conda create --help` |
| Show conda info | `conda info` | `conda info` |

---

## 🔹 Create Environments

| Task | Command | Example |
| :-- | :-- | :-- |
| Create empty env (no packages) | `conda create -n <name>` | `conda create -n myenv` |
| Create with latest Python | `conda create -n <name> python` | `conda create -n myenv python` |
| Create with specific Python | `conda create -n <name> python=<ver>` | `conda create -n py311 python=3.11` |
| Create with Python and packages | `conda create -n <name> python=<ver> <pkg> ...` | `conda create -n ds python=3.10 numpy pandas jupyter` |
| Create with package versions | `conda create -n <name> <pkg>=<ver> ...` | `conda create -n sci scipy=1.11 matplotlib=3.8` |
| Create from YAML | `conda env create -f environment.yml` | `conda env create -f environment.yml` |
| Create at custom path | `conda create --prefix <path> ...` | `conda create --prefix ./envs/proj python=3.11` |
| Create targeting a platform | `conda create --platform <subdir> -n <name> ...` | `conda create --platform osx-64 -n pyx64 python` |

---

## 🔹 Activate / Deactivate

| Task | Command | Example |
| :-- | :-- | :-- |
| Activate by name | `conda activate <name>` | `conda activate myenv` |
| Activate by path | `conda activate <path>` | `conda activate ./envs/proj` |
| Deactivate current env | `conda deactivate` | `conda deactivate` |

---

## 🔹 List Environments & Packages

| Task | Command | Example |
| :-- | :-- | :-- |
| List environments | `conda env list` | `conda env list` |
| List packages in current env | `conda list` | `conda list` |
| List packages in named env | `conda list -n <name>` | `conda list -n myenv` |
| Show envs via info | `conda info --envs` | `conda info --envs` |

---

## 🔹 Install, Update, Remove Packages

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

---

## 🔹 Remove, Clone, Export Environments

| Task | Command | Example |
| :-- | :-- | :-- |
| Remove env by name | `conda remove -n <name> --all` | `conda remove -n myenv --all` |
| Remove env (subcommand) | `conda env remove -n <name>` | `conda env remove -n myenv` |
| Remove env by path | `conda remove --prefix <path> --all` | `conda remove --prefix ./envs/proj --all` |
| Clone environment | `conda create --clone <src> -n <dest>` | `conda create --clone ds -n ds-copy` |
| Export YAML | `conda env export -n <name> > environment.yml` | `conda env export -n ds > environment.yml` |
| Export explicit lockfile | `conda list --explicit > pkgs.txt` | `conda list --explicit > pkgs.txt` |
| Create from explicit file | `conda create -n <name> --file pkgs.txt` | `conda create -n exact --file pkgs.txt` |

---

## 🔹 Exporting an Environment to YAML

<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" alt="conda logo" height="64" />

If you already have an environment named **`p`** and want to export it to `environment.yml`:

- **On Windows (PowerShell):**
  ```powershell
  conda activate p; conda env export > environment.yml
````

* **On macOS/Linux (bash/zsh):**

  ```bash
  conda activate p && conda env export > environment.yml
  ```

💡 **Tip:** To only include explicitly installed packages (cross-platform minimal spec):

```bash
conda activate p && conda env export --from-history > environment.yml
```

📚 References:

* [Conda export docs](https://docs.conda.io/projects/conda/en/stable/commands/env/export.html)
* [StackOverflow discussion](https://stackoverflow.com/questions/41274007/anaconda-export-environment-file)
* [Exporting from history explanation](https://www.monicathieu.com/posts/2024-05-20-conda-env-export-from-history.html)

---

## 🔹 Revisions & Rollback

| Task                       | Command                            | Example                        |
| :------------------------- | :--------------------------------- | :----------------------------- |
| List history (current env) | `conda list --revisions`           | `conda list --revisions`       |
| Roll back to a revision    | `conda install --revision <num>`   | `conda install --revision 3`   |
| List history (named env)   | `conda list -n <name> --revisions` | `conda list -n ds --revisions` |

---

## 🔹 Quality-of-Life Flags

| Use case                        | Flag                    | Example                                              |
| :------------------------------ | :---------------------- | :--------------------------------------------------- |
| Auto-confirm actions            | `-y`                    | `conda create -n ds python=3.10 -y`                  |
| Create without default packages | `--no-default-packages` | `conda create -n clean python --no-default-packages` |
| Specify channels inline         | `-c <channel>`          | `conda install -c conda-forge mamba`                 |

---

## 🔹 Minimal End-to-End Examples

* Create simple env with latest Python:

  ```bash
  conda create -n simple python -y
  conda activate simple
  ```

* Env with Python 3.11 and packages:

  ```bash
  conda create -n ml python=3.11 numpy pandas scikit-learn jupyter -y
  conda activate ml
  ```

* Export and recreate:

  ```bash
  conda env export -n ml > environment.yml
  conda env remove -n ml
  conda env create -f environment.yml
  ```

* Delete an environment:

  ```bash
  conda remove -n simple --all
  ```

---

## 🔹 Conda vs Pip (Super Simple)

| Tool      | What it installs               | Manages environments? | Typical use case           |
| :-------- | :----------------------------- | :-------------------- | :------------------------- |
| **Conda** | Any software (not just Python) | ✅ Yes                 | Data science, mixed stacks |
| **Pip**   | Python packages only           | ❌ No (use venv)       | Pure Python projects       |

👉 If you want non-Python packages or easy environment management → **use Conda**.
👉 If you only need Python packages → **pip is enough**.

---

## 🔹 `pip install` vs `conda install`

| Command         | Installs                         | Works in        | Handles non-Python stuff? | Manages environments? |
| :-------------- | :------------------------------- | :-------------- | :------------------------ | :-------------------- |
| `pip install`   | Python packages only             | Any Python env  | ❌ No                      | ❌ No (use venv)       |
| `conda install` | Any package (Python, R, C, etc.) | Conda envs only | ✅ Yes                     | ✅ Yes                 |

**Rule of thumb:**

* Use `conda install` first inside conda envs.
* If package not available, then use `pip install`.

---

## 🔹 Add Conda-Forge Channel

```bash
# Add conda-forge as highest priority channel
conda config --add channels conda-forge

# Set strict channel priority
conda config --set channel_priority strict

# Show channel list
conda config --show channels

# One-time install from conda-forge
conda install -c conda-forge <package>
```

---

## 📚 References

* [Conda docs — Managing environments](https://docs.conda.io/projects/conda/en/stable/user-guide/tasks/manage-environments.html)
* [Conda commands index](https://docs.conda.io/projects/conda/en/stable/commands/index.html)
* [Conda vs Pip (Anaconda Blog)](https://www.anaconda.com/blog/understanding-conda-and-pip)
* [Conda-forge docs](https://conda-forge.org/docs/user/introduction/)

---

⭐ If you find this useful, star the repo for quick access later!

```

---

Do you also want me to **add a quick badge block** at the very top (like Python, Conda, License, Made with ❤️, etc.), so it looks more polished when viewed on GitHub?
```
