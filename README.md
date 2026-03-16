# Pair Extraordinaire Achievement Collector

Automate the creation of **co-authored pull requests** using GitHub
Actions to unlock the **Pair Extraordinaire** GitHub achievement.

This repository contains a workflow that automatically:

1.  Creates commits with two authors
2.  Opens pull requests into `main`
3.  Squash merges them
4.  Deletes the branch
5.  Repeats the process multiple times

The workflow is designed to help demonstrate **co‑authored collaboration
activity** using GitHub automation.

------------------------------------------------------------------------

# What this project does

The workflow generates a sequence of pull requests where each commit
includes:

-   a primary author
-   a co-author using the `Co-authored-by:` commit trailer

GitHub recognizes these commits as collaborative contributions.

When merged, they count toward the **Pair Extraordinaire** achievement.

------------------------------------------------------------------------

# How the workflow works

When the workflow runs, it performs the following steps:

1.  Checks out the `main` branch with full history
2.  Installs the GitHub CLI (`gh`)
3.  Authenticates using a Personal Access Token
4.  Ensures a placeholder file `.envexample` exists
5.  Loops through multiple iterations
6.  Creates a commit authored by one user
7.  Adds a `Co-authored-by:` trailer for the second user
8.  Pushes the branch
9.  Creates a pull request
10. Squash merges the PR
11. Deletes the branch
12. Repeats the process

Each iteration updates `.envexample` to guarantee a real file change.

------------------------------------------------------------------------

# Repository requirements

Before running this workflow:

-   GitHub Actions must be enabled
-   Your repository must have a `main` branch
-   The token must have permission to push and merge PRs
-   Branch protection rules must allow the workflow to merge

This workflow should be used in a **repository you control**.

------------------------------------------------------------------------

# Setup

## 1. Add the workflow file

Create the file:

    .github/workflows/pair-extraordinaire.yml

Paste the workflow contents into that file.

------------------------------------------------------------------------

## 2. Create a Personal Access Token

Create a GitHub **Personal Access Token** that allows:

-   repository read/write
-   pull request creation
-   pull request merging

Typical permission scope:

    repo

------------------------------------------------------------------------

## 3. Add the token as a repository secret

In your repository:

1.  Open **Settings**
2.  Navigate to **Secrets and Variables**
3.  Click **Actions**
4.  Create a secret named:

```{=html}
<!-- -->
```
    PERSONAL_ACCESS_TOKEN

Paste the token value.

------------------------------------------------------------------------

# Usage

This workflow is triggered manually.

Steps:

1.  Open the **Actions** tab in your repository
2.  Select **Automate Pair Extraordinaire Badge**
3.  Click **Run workflow**

The workflow will then automatically generate and merge the configured
number of co-authored pull requests.

------------------------------------------------------------------------

# Workflow configuration

Inside the workflow you will see configuration values such as:

    COAUTHOR_NAME
    COAUTHOR_EMAIL
    PRIMARY_NAME
    PRIMARY_EMAIL

These values define the two collaborators.

Example:

    COAUTHOR_NAME: DongwanXu
    COAUTHOR_EMAIL: dongwanxu23@gmail.com

    PRIMARY_NAME: chrisbanas
    PRIMARY_EMAIL: bananas595@gmail.com

Both emails must be **verified emails on the respective GitHub
accounts**.

Otherwise GitHub will not recognize the co-author.

------------------------------------------------------------------------

# How commits are structured

Each commit uses the format:

    Author: DongwanXu
    Co-authored-by: chrisbanas

GitHub parses the trailer:

    Co-authored-by: Name <email>

This is how the contribution is attributed to both accounts.

------------------------------------------------------------------------

# File changes made

Each iteration appends a line to:

    .envexample

Example:

    BADGE_RUN_12=1712345678

This guarantees that each PR contains a real commit.

------------------------------------------------------------------------

# Loop count

The workflow runs approximately **48--49 pull request cycles**.

This number can be adjusted inside the script if desired.

Example loop:

    for i in $(seq 1 49)

------------------------------------------------------------------------

# Rate limiting

The workflow includes a short delay between merges:

    sleep 1

This helps prevent GitHub API rate limits.

If you encounter limits, increasing this delay may help.

------------------------------------------------------------------------

# Branch naming

Temporary branches are created like:

    badge-run-1
    badge-run-2
    badge-run-3

These are deleted automatically after merging.

------------------------------------------------------------------------

# Security notes

Best practices:

-   never store tokens directly in the workflow file
-   always use repository secrets
-   use minimal token permissions
-   test in a personal repository first

------------------------------------------------------------------------

# Public repository note

If this project is public:

-   commit history will show automated PR activity
-   collaborators will appear in commit authorship
-   the workflow logic will be visible

Never expose your personal access token.

------------------------------------------------------------------------

# Recommended testing

Before running a full batch, you may want to reduce the loop count:

    seq 1 3

This allows you to verify:

-   authentication works
-   commits are created correctly
-   PR creation works
-   merging works
-   branch deletion works

Once confirmed, increase the count.

------------------------------------------------------------------------

# Disclaimer

Use this workflow responsibly and only in repositories you control or
have permission to automate.

You are responsible for complying with GitHub's platform policies and
repository rules.
