# `lib-quickstart-template` - Quickstart Template

A ready-to-use template containing everything you need to start developing your own DAX Lib library.

## 🚀 Getting Started

### 1. Create a New Repository from this Template

- Click [![Use this template](https://img.shields.io/badge/Use%20this%20template-brightgreen?logo=github)](https://github.com/daxlib/lib-quickstart-template/generate) to create your new repository based on this template.
- Enter a repository name that reflects the name of the library you want to develop.

> [!TIP]
> Need to develop more libraries? Simply reuse this template and generate a new repository for each one.

### 2. Fork the DAX Lib repository

- If you already created a fork of the [DAX Lib](https://github.com/daxlib/daxlib) repository, you can skip this step.
- Click [![Fork](https://img.shields.io/badge/Fork-brightgreen?logo=github)](https://github.com/daxlib/daxlib/fork) to create a fork of the official [DAX Lib](https://github.com/daxlib/daxlib) repository.
- Keep the default name `daxlib` for your fork. Need a different name? [See FAQ](#why-keep-the-fork-name-as-daxlib)
- Your fork will be created in your GitHub account

> [!NOTE]
> See [FAQ](#-faq) for why a fork is needed and how to manage it.

## ⚙️ Repository Setup

Follow these steps to configure your new repository:

### 1. Create a Personal Access Token (PAT)

- Go to [GitHub PAT settings](https://github.com/settings/personal-access-tokens/) in your GitHub account and click **Generate new token**
- Configure the token with these settings:
  - **Token name**: `DAXLIBFORK_PAT`
  - **Description**: `Token for pushing changes to my DAX Lib fork` (or any description you prefer)
  - **Resource owner**: your GitHub account
  - **Expiration**: choose `No expiration` or set a date (remember to renew before expiry)
  - **Repository access**: select `Only select repositories`, then choose your forked `daxlib` repository
- Set permissions:
  - Click `+ Add permissions`
  - Select `Contents`
  - Change access level from `Read-only` to `Read and write`
- Click **Generate token**
- Copy the token (PAT) and store it securely - you won't be able to see it again once you leave the page

### 2. Add the Token to Your Repository

- Open the **Settings** tab of your new repository (the one created from this template)
- Navigate to **Secrets and variables** → **Actions** in the left sidebar
- Click **New repository secret**
- Add the secret:
  - **Name**: `DAXLIBFORK_PAT`
  - **Secret**: Paste the Personal Access Token (PAT) you created earlier
- Click **Add secret**

## 🧩 Customize Your Library

The template includes a boilerplate library called `Contoso.Sample`. Customize it for your needs:

- Update library metadata: edit `src/manifest.daxlib` to set your library's name, version and other metadata
- Add your functions: edit `src/lib/functions.tmld` to define your library's functions

## 📦 Publish Your Library

Once your code is ready, you can publish a new version:

- Go to the **Actions** tab in your repository
- Select the `publish-package` workflow from the left sidebar
- Click **Run workflow** and confirm
- Wait for the workflow to complete
- After completion, a summary will appear with a link to create a pull request to the official DAX Lib repository
- Click the link to open your pull request, add a description, and submit it for review
- If you make further changes, re-run the workflow to update the pull request automatically

> [!TIP]
> You can iterate on your changes as many times as needed before the pull request is merged. Just keep the same library version in `manifest.daxlib`, and each workflow run will update the same pull request.

Your pull request will be reviewed by the DAX Lib maintainers and, if changes are requested during the review:

- Apply the requested fixes to your code and commit them to your repository
- Re-run the `publish-package` workflow
- The pull request will be automatically updated

Once your pull request is approved and merged, your library will be automatically published on [daxlib.org](https://daxlib.org/).

## 📚 Resources

- [DAX Lib documentation](https://docs.daxlib.org/)
- [DAX Lib repository](https://github.com/daxlib/daxlib)

## ❓ FAQ

### What is a fork and why do I need one?

A fork is a personal copy of another repository on GitHub. In this case, you need a fork of the DAX Lib repository to create a pull request from your library repository to the official DAX Lib repository. If you create multiple libraries from this template, only one fork is needed for all of them.

### How does the workflow use my fork?

The workflow in your repository uses the Personal Access Token (PAT) you created to authenticate and push changes to your fork of the DAX Lib repository. It creates a branch in your fork with the changes from your library and then generates or updates a pull request to the official DAX Lib repository.

### Why keep the fork name as `daxlib`?

We recommend keeping the fork name as `daxlib` to simplify configuration. If you choose a different name, make sure to update the `DAXLIBFORK_NAME` variable in the workflow file `.github/workflows/publish-package.yml`.

### How do I manage my fork?

- **Don't make manual changes to the fork** - it's managed automatically by the workflow.
- **(optional) Sync the fork before publishing** - this ensures you're working with the latest DAX Lib release.
- **(optional) Branch cleanup** - each pull request creates a branch in the fork. You can delete these after approval.
