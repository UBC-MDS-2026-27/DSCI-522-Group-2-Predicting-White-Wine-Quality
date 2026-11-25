# Contributing to Predicting White Wine Quality

This document provides guidelines for reporting bugs, suggesting changes, and submitting contributions (include AI usage instructions) to the Predicting White Wine Quality project. It also explains how to set up your computer, how to work on the project inside our Docker container, how to add or update a package, and how to publish the report.

## Fixing typos

Small typos or grammatical errors in documentation may be edited relevant source files on a separate branch (not directly on main branch). The submission of all changes, including minor fixes, must be using a branch assotiated with a pull request rather than merge onto the main branch directly.

## Reporting Bugs and Suggesting Changes

* Bug reporting: Open a GitHub issue describing the problem you encountered and followed by steps to reproduce it. Include the difference between the expected results and the actual results. Please include as much details as possible for us to reproduce the bug.

* Change Suggestion: Open a GitHub issue describing the change you suggest and also the reasoning behind such change. Please be specific about why the change you suggest may have the potential to benefit the project. Furthermore, for substential changes please discuss with the project team first before creating the GitHub issue.

## Submitting Contributions

Please follow the GitHub workflow mentioned below for submitting contributions (including small adjustments mentioned above):

* Open an issue: Please open a GitHub issue first before starting your work, so there's a chance to discuss your opinion with the project team and track your progress clearly.
* Create a branch: Create a new branch with meaningful name which shows the purpose of the contribution from the updated main branch.
* Implement changes: Do your work inside our Docker container (see [Working in the Container with Positron](#working-in-the-container-with-positron)). The work should stay on your own branch so it does not affect others' work.
* Commit and push: Please use meaningful commit message (but stay short) to inform others regarding the change, and then push your branch.
* Open a pull request and review: As mentioned earlier, a pull request is expected and please add reviewers from the project team to review and approve the changes before merging into main.
* Merge: Once the changes have been reviewed and approved, the pull request can be merged into main.

## Setting up your Computer

The setup steps (making an ssh key and downloading our Docker image with `docker compose pull`) are described in the [README](README.md). Please follow them first, and make sure [Docker](https://www.docker.com/get-started/) is installed and running.

In addition, you need two things that are only required for contributing:

1. **Positron:** Install [Positron](https://positron.posit.co/download.html). Its Remote SSH feature, which we use to connect to the container, is built in, so you do not need to install an extension.
2. **Your Git name and email:** In a terminal on your computer, run `git config --global user.email`. It should print the email address of your GitHub account. If it prints nothing, set your name and email with `git config --global user.name "Your Name"` and `git config --global user.email "you@example.com"`. Our `docker-compose.yml` shares these settings with the container, so the commits you make there count as yours.

Make the ssh key and set your Git name and email **before** you start the container for the first time. Otherwise, Docker creates empty folders in their place, and you will have to delete them before you can connect (see [Troubleshooting](#troubleshooting)).

## Working in the Container with Positron

All work on the project should be done inside our Docker container, so that everyone uses exactly the same software and package versions. We connect to the container from Positron over ssh. Your project folder is shared with the container at `/workspace`, so any file you change in the container also changes on your computer.

1. In a terminal on your computer, go to the project folder and start the container in the background:

   ```bash
   docker compose up -d
   ```

   You can check that it is running with `docker compose ps`, which should list `analysis-env`.

2. In Positron, open the Command Palette (`Cmd+Shift+P` on Mac, `Ctrl+Shift+P` on Windows), run **Remote SSH: Show Remote Menu**, and choose **Connect to Host**.

3. Type `root@localhost:2222` and press Enter. A new Positron window opens. If Positron asks for the platform of the remote host, choose **Linux**, and if it asks whether you trust the host's fingerprint, click **Continue**. The first time you connect, Positron installs its server inside the container, which can take more than five minutes.

4. Once you are connected, the bottom left corner shows `SSH: localhost:2222`, but no folder is open yet. Click **Open Folder** in the Explorer, replace the path with `/workspace`, and press Enter (you may need to click **OK** more than once). The window reloads and the Explorer shows the project files.

5. Positron opens the folder in **Restricted Mode**, in which consoles cannot start. Click **Manage** in the banner at the top of the window (or **Trust this folder** in the Console) and choose to trust the folder. If Positron then offers to run `uv sync`, choose **No**: the project's environment is already installed in the container at `/opt/venv`, and running `uv sync` would create an extra `.venv` folder in the project.

6. Choose the project's Python interpreter. Positron may start the container's system Python (`/usr/bin/python3`), which does not have our packages, so check this every time. Click the interpreter button at the top right of the window and choose **New Console Session…**. Pick the interpreter at `/opt/venv/bin/python`, which is built from our `uv.lock`. Do not pick `/usr/bin/python3` or `/workspace/.venv`. If `/opt/venv/bin/python` is not in the list, open the Command Palette, run **Python: Select Interpreter**, choose **Enter interpreter path…**, and type `/opt/venv/bin/python`. It will then appear in the list. To check that you have the right interpreter, run the following in the Console, which should print `/opt/venv/bin/python`:

   ```python
   import sys; print(sys.executable)
   ```

7. Work as usual. The Terminal, the Console and the **Render** button all run inside the container. To render the report from the Terminal, run:

   ```bash
   uv run quarto render analysis/white-wine-quality.qmd
   ```

8. When you are done, close the Positron window, then stop the container in a terminal on your computer:

   ```bash
   docker compose down
   ```

### Troubleshooting

* **`~/.ssh/id_ed25519.pub` is a folder.** Docker created it because your ssh key did not exist yet. Run `docker compose down`, delete that folder, make the key as described in the [README](README.md), and start again.
* **`~/.gitconfig` is a folder, or Git in the container does not know your name.** The same thing happened with your Git settings. Run `docker compose down`, delete that folder, set your Git name and email as described above, and start again.
* **Positron asks for a password.** The container cannot see your ssh key. Check that your key is named `id_ed25519.pub`, or change the key path in `docker-compose.yml`.
* **GitHub asks you to sign in when you push from the container.** Sign in once in the browser window that Positron opens. Positron remembers it.
* **"Remote host identification has changed".** You are using a new image. Run `ssh-keygen -R "[localhost]:2222"` on your computer, then connect again.
* **Port 2222 is already in use.** Change the first `2222` in `docker-compose.yml` to another number (for example, `2223`) and connect to that port instead. Do not commit this change.
* **Linux laptops: ssh refuses the key.** On Linux, the mounted key file belongs to you rather than to `root`. Remove the `#` from the `StrictModes no` line in the `Dockerfile` and push the change on a branch, so that GitHub Actions publishes a fixed image.
* **Consoles do not start, or Positron says the Python extension is not available.** The folder is still in Restricted Mode. Trust the folder as described in step 5. If the message remains, wait a minute or run **Developer: Reload Window** from the Command Palette.

## Adding or Updating a Package

Our Docker image is built from `pyproject.toml` and `uv.lock`, so a new package must be added to these files and published in a new image. Every package in `pyproject.toml` must be pinned to an exact version with `==`.

1. Create a new branch from `main`.
2. Add the package with uv, pinning its version, for example `uv add "pandas==2.3.3"`. This updates both `pyproject.toml` and `uv.lock`.
3. Commit `pyproject.toml` and `uv.lock` together and push the branch.
4. GitHub Actions builds and publishes a new image on Docker Hub, then commits the new image tag to `docker-compose.yml` on your branch. You can follow its progress in the **Actions** tab of the repository.
5. When the workflow has finished, run `git pull` to get the updated `docker-compose.yml`, then `docker compose pull` to download the new image. Restart the container with `docker compose down` and `docker compose up -d`, and check that the new package works.
6. Open a pull request and have it reviewed and merged.
7. The merge into `main` builds the image once more and commits a new tag to `main`. When that workflow run has finished, everyone should run `git pull` on `main` and then `docker compose pull`.

## Publishing the Report

Our report is published on GitHub Pages from the `docs/` folder on the `main` branch. The published file, `docs/index.html`, is a copy of the rendered report, so it does not update by itself. Each time you change the report, render it again inside the container and copy it into `docs/`:

```bash
uv run quarto render analysis/white-wine-quality.qmd
cp analysis/white-wine-quality.html docs/index.html
```

Then commit `docs/index.html` on your branch and include it in your pull request. After the pull request is merged into `main`, GitHub Pages updates the published report within a few minutes.

## AI Policy

Most importantly, pull requests and issues must be opened by a human, not by an AI agent or chat bot. You may use AI agents to help double-check code before merging pull requests. Please always cite the AI tools you used and describe how you used such AI tools.

Below is a more generalized adapted AI Policy:

### Scope

* "AI" herein refers to generative AI tools like large language models (LLMs) that can generate, edit, and review software code, create and manipulate images, or generate human-like communication. This policy applies to contributions from the wider community. Automated processes operated by the project maintainer team (for example, dependency updates and other repository automations) run under separate maintainer oversight and are not governed by the requirements below.

### Responsibility

* You must understand and be able to explain both the code you submit and the existing related code; submitting a patch you cannot explain yourself is not acceptable. The explanation must be yours, though you may use AI to translate or copy-edit it.

* The use of an AI agent that writes code and then submits a pull request autonomously is not permitted. A human must check any generated code and open the pull request themselves as stated at the beginning of the AI policy section.

## Code of Conduct

Please note that this project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

## Attribution

This contribution guide was adapted from the [dplyr Contribution Guidelines](https://github.com/tidyverse/dplyr/blob/main/.github/CONTRIBUTING.md).

The AI Usage Policy was adapted from the [earthaccess AI Policy](https://earthaccess.readthedocs.io/en/latest/contributor/ai-policy/).

The instructions for working in the container were adapted from the DSCI 522 Milestone 2 instructions and [docker-uv-renv](https://github.com/chendaniely/docker-uv-renv) by Daniel Chen.