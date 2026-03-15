---
title: "Contribute"
layout: single
permalink: /contribute
---

We are always open to updating and extending the guidelines and are waiting for your input!

All sources of this webpage are hosted on GitHub at [ros-rvft.github.io](https://github.com/ros-rvft/ros-rvft.github.io). Contributions can be submitted directly to our GitHub repository. Here's how to do it!

### Step 1: Fork

Fork the [project](https://github.com/ros-rvft/ros-rvft.github.io) on GitHub and clone your fork locally. Make sure you do so from the 'main' branch.

```
git clone https://github.com/ros-rvft/ros-rvft.github.io
```

### Step 2: Branch

Create a branch and start writing! You can modify existing guidelines, or propose a new one starting from our [guideline template](https://github.com/ros-rvft/ros-rvft.github.io/blob/main/guideline_template.html).

```
git checkout -b my-branch -t origin/main
```

### Step 3: Commit

Submit all of your changed files and commit!

```
git add my/changed/files
git commit
```

### Step 4: Push

Push your commits to the repository, creating a pull request to the main branch.

```
git push origin my-branch
```

### Step 5: Discuss

After the pull request was created, keep track of it on GitHub where you can discuss your contributions with the team!

![Contribution workflow](/img/contrib.png)

### Step 6: Merge

The pull request review is finished and the final version of your contribution is added to the guidelines!

Here's an example of a contribution: [Feedback Pull Request](https://github.com/ros-rvft/ros-rvft.github.io/pull/1)

Feel free to fork and make additions directly to the source files. Create a pull request and we'll begin discourse in the reviewing process!

You can also forward suggestions directly to [ricardo.caldas@gssi.it](mailto:ricardo.caldas@gssi.it)!

## What Makes a Good Contribution?

We welcome several kinds of contributions:

- **New tools or techniques:** Know a runtime verification tool, testing framework, or specification language for ROS that we haven't covered? Suggest it! You can [open a GitHub Issue](https://github.com/ros-rvft/ros-rvft.github.io/issues/new/choose) describing the tool and which guideline it relates to — no need to write HTML.
- **Updates to existing guidelines:** Tools evolve. If a tool we reference has a new version, new features, or has been superseded, let us know.
- **New worked examples:** Practical examples showing how to apply a guideline with a specific tool are especially valuable.
- **Corrections and improvements:** Typos, broken links, unclear wording — all welcome.

### Lightweight contribution (no Git required)

If you don't want to fork and PR, you can simply [open a GitHub Issue](https://github.com/ros-rvft/ros-rvft.github.io/issues/new/choose) and pick from one of our templates:

- **Suggest a Tool or Technique** — for new tools we should cover.
- **Update an Existing Guideline** — for corrections, new versions, broken links.
- **Report a Gap** — for topics or practices the guidelines should address.

No Git, no HTML, no forking required.
