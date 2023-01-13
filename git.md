# Git

## Table of contents

1. [Overview](#overview)
2. [Git Commands](#git-commands)
   1. [init](#init)
   2. [add](#add)
   3. [commit](#commit)
   4. [clone](#clone)
   5. [status](#status)
   6. [config](#config)
   7. [push](#push)
   8. [pull](#pull)
   9. [remote](#remote)
   10. [fetch](#fetch)
3. [Working as a team](#working-as-a-team)
   1. [Github](#github)
   2. [Avoiding Conflicts](#avoiding-conflicts)
   3. [Branches](#branches)
4. [FAQ](#faq)
   1. [I can't see a branch?](#i-cant-see-a-branch)
   2. [How do I keep my branch up to date?](#how-do-i-keep-my-branch-up-to-date)
   3. [How do I rename my last commit?](#how-do-i-rename-my-last-commit)
   4. [How do I add changes to my last commit?](#how-do-i-add-changes-to-my-last-commit)
   5. [How do I rename, or combine commits?](#how-do-i-rename-or-combine-commits)
   6. [How do I solve a merge conflict?](#how-do-i-solve-a-merge-conflict)

## Overview

![Overview](https://user-images.githubusercontent.com/48181323/212286657-c22de3e2-4061-48dd-922e-a3cecd74ce30.svg)

## Git Commands

### init

The `git init` command is used for adding git to a project or folder. The command creates a new subdirectory named `.git` which contains all repository files.

#### Usage

```sh
git init <optional name>
```

### add

The `git add` command is used for tracking a files changes, this is also called staging. The command accepts wildcards `*` in the files path allowing you to add multiple files at once. You can also add an entire directory and its contents using a relative such as `.` or `..`.

#### Usage

```sh
git add <path>
```

### commit

The `git commit` command is used for saving the tracked changes to the git repository. You can use the `-m <title>` argument for directly specifying a commit title. If ommitted it will just open your default text editr as specified in git and ask you to input a name or accept the default one, which is the name of a file you've edited.

#### Usage

```sh
git commit [args]
```

### clone

The `git clone` command is used for for downloading, cloning, an existing repository. You can use the `--branch <name>` argument to specify which branch of the repositroy it should clone.

#### Usage

```sh
git clone <url> [args]
```

### status

The `git status` command is used for displaying the current status of the repository. It will show files modified, removed or added files and if they're staged for commit.

#### Usage

```sh
git status
```

### config

The `git config` command is used for changing a git setting. This can be done globally or done per repository (see the `--global` and `--local`) flags. Two common settings are the username and email which can be specified with `user.name` and `user.email` setting.

#### Usage

```sh
git config [--global, --local] <setting> <value>
```

### push

The `git push` command is used for sending commits stored in the local repository to the remote repository, for example Github.

#### Usage

```sh
git push <remote> <branch>
```

### pull

The `git pull` command is used for fetching changes of the remote repository and then merging them with the existing changes in the local repository.

#### Usage

```sh
git pull <remote> <branch>
```

### remote

The `git remote` command is used for viewing and specifying remote servers that host your git repository. If you've cloned a repository it will show a remote called `origin`, which is the server you cloned from.

#### Usage

```sh
git remote [add <name> <url>, remove <name>, rename <old name> <new name>]
```

### fetch

The `git fetch` command is used for fetching changes from the remote repository. You can merge this changes with your local ones at a later time. The `git pull` command will fetch and merge in one command.

#### Usage

```sh
git fetch <remote>
```

## Working as a team

### Github

Github is a website that works as your remote origin and allows you to host and share your git repositories. It includes useful features such as keeping track of issues, pull requests and you can even create your own wiki page.

To login to git with github you can use the [Github CLI](https://cli.github.com/)

When it's installed run the following:

```sh
gh auth login
gh auth setup-git
```

### Avoiding conflicts

A good way to avoid conflicts and keeping the code clean and structured is to split it in to multiple files. For example if you're working on a frontend application you can split commonly used components in to multiple files.

Another good way is to communicate with your team so everyone knows what you're working on. This lowers the risk that you might run in to a conflict my changing the same file.

### Branches

To prevent interfearing with others work and to keep the code organised, there are multiple branches.

There are generally four types of branches:

- main is the production branch containing the code for the latest "stable" builds of your project.

- dev is the development branch containing the latest bleeding edge features.

- feat/ indicates a feature branch. This is where a new feature is being developed. For example the name could be `feat/user-authentication`, which means this branch contains work in progress code of an user authentication feature.

- fix/ indicates that it's a bug fix branch. It works much the same way as the feature branch but it contains work in progress code for bug fixes.

When a `feat` or `fix` branch is completed it should be pulled in to the dev branch for further testing and then be deleted.

## FAQ

### I can't see a branch?

Make sure you've fetched the latest information from the remote repository by using [git fetch](#fetch).

### How do I keep my branch up to date?

To update your branch you can rebase it, which means to put your commits on top of a remote branchs. You can do so with the [git pull](#pull) command and the rebase argument. See the [git pull](#pull) section for more information on how to rebase.

### How do I rename my last commit?

You can use the `--amend` argument together with the `-m` argument in the [git commit](#commit) command.

### How do I add changes to my last commit?

You can use the `--amend` argument argument in the [git commit](#commit) command.

### How do I rename, or combine commits?

If you're trying to rename your last commit, click [here](#how-do-i-rename-my-last-commit).

If not, you can use the git rebase command with the interactive flag. Though be careful so you don't accidentally break anything.

```sh
git rebase -i HEAD~<number_of_commits>
```

### How do I solve a merge conflict?

When a git merge fails it adds three sets of seven symboles indicating what it is that's conflicting.

- `<<<<<<<` (seven "less than" characters) followed by HEAD, which is an alias for the current branch. The symbols indicate the beginning of the edits within this section.
- `=======` (seven "equals sign" characters), which show the end of the revisions within the current branch and the beginning of the edits within a new one.
- `>>>>>>>` (seven "greater than" characters) followed by the branch where the attempted merge happened. The added symbols indicate the ending of the edits within the conflicting branch.

You can then choose the code to keep and make a new commit to solve the conflict.
