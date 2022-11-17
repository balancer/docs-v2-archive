# Contribution Guide

## General <a href="#general" id="general"></a>

Balancer is an open-source protocol and consists of a number of repositories on [Github](https://github.com/balancer-labs/). Contributions are always welcome!

### Commit Messages <a href="#commit-messages" id="commit-messages"></a>

Contributors **should** adhere to the following standards and best practices when making commits to be merged into the Balancer codebase.

**Conventional Commits**

Commit messages **should** adhere to the standard. A conventional commit message is structured as follows:

`<type>[optional scope]: <description>`

`​[optional body]`

`​[optional footer]`

The commit contains the following elements, to communicate intent to the consumers of your library:

* **fix**: a commit of the _type_ `fix` patches a bug in your codebase (this correlates with `PATCH` in semantic versioning).
* **feat**: a commit of the _type_ `feat` introduces a new feature to the codebase (this correlates with `MINOR` in semantic versioning).
* **BREAKING CHANGE**: a commit that has the text `BREAKING CHANGE:` at the beginning of its optional body or footer section introduces a breaking API change. A BREAKING CHANGE can be part of commits of any _type_.

The use of commit types other than `fix:` and `feat:` is recommended. For example: `docs:`, `style:`, `refactor:`, `test:`, `chore:`, or `improvement:`.

**Best Practices**

The following best practices are recommended for writing commit messages (adapted from [How to Write a Commit](https://cbea.ms/git-commit/)):

* Limit the subject line to 50 characters.
* Use imperative, present tense in the subject line.
* Capitalize the subject line.
* Do not end the subject line with a period.
* Separate the subject from the body with a blank line.
* Wrap the body at 72 characters.
* Use the body to explain what and why vs. how.

### GitHub Standard Fork and Pull Request Workflow <a href="#github-standard-fork-and-pull-request-workflow" id="github-standard-fork-and-pull-request-workflow"></a>

_Original version: https://gist.github.com/Chaser324/ce0505fbed06b947d962_

When it comes to open source contributions, knowing how to properly fork and generate _a pull request_ is essential. Unfortunately, it is fairly easy to make mistakes or not know what to do, especially when doing this for the first time. In the following lines, there is a short tutorial on a standard procedure to create a fork, do some work, create a pull request, and merge the pull request back into the original project.

**Creating a Fork**

Just head over to the GitHub page and click the “Fork” button. After that, you can use your favourite git client to clone your repo or just head straight to the command line:

`# Clone your fork to your local machine`

`git clone git@github.com:USERNAME/FORKED-PROJECT.git`

**Keeping Your Fork Up to Date**

While this is not always a necessary step, if you plan to do more than just a tiny quick fix, you’ll want to make sure you keep your fork up to date by tracking the original “upstream” repo that you forked. To do this, you’ll need to add a remote:

`# Add 'upstream' repo to list of remotes`

`git remote add upstream https://github.com/UPSTREAM-USER/ORIGINAL-PROJECT.git​`

`# Verify the new remote named 'upstream'`

`git remote -v`

Whenever you want to update your fork with the latest upstream changes, you’ll need to first fetch the upstream repo’s branches and latest commits to bring them into your repository:

`# Fetch from upstream remote`

`git fetch upstream​`

`# View all branches, including those from upstream`

`git branch -va`

Now, checkout your own master branch and merge the upstream repo’s master branch:

`# Checkout your master branch and merge upstream`

`git checkout master`

`git merge upstream/master`

If there are no unique commits on the local master branch, git will simply perform a fast-forward. However, if you have been making changes on master (in the vast majority of cases you probably shouldn’t be), you may have to deal with conflicts. When doing so, be careful to respect the changes made upstream.

Now, your local master branch is up-to-date with everything modified upstream.

### Doing Your Work

#### Create a Branch

Whenever you begin to work on a new feature or bugfix, it is important that you create a new branch. Not only is it a proper git workflow, but it also keeps your changes organized and separated from the master branch so that you can easily submit and manage multiple pull requests for every task you complete.

To create a new branch and start working on it:

`# Checkout the master branch - you want your new branch to come from master`

`git checkout master​`

`# Create a new branch named newfeature (give your branch its own simple informative name)`

`git branch newfeature`

`​# Switch to your new branch`

`git checkout newfeature`

Now, go ahead and implement the changes that you want.

### Submitting a Pull Request

#### Cleaning Up Your Work

Before submitting your pull request, you might want to do a few things to clean up your branch and make it as simple as possible for the original repo’s maintainer to test, accept, and merge your work.

If any commits have been made to the upstream master branch, you should rebase your development branch so that merging it will be a simple fast-forward that will not require any conflict resolution work.

`# Fetch upstream master and merge with your repo's master branch`

`git fetch upstream`

`git checkout master`

`git merge upstream/master`

``

`​# If there were any new commits, rebase your development branch`

`git checkout newfeature`

`git rebase master`

Now, it may be desirable to combine (squash) some of your smaller commits down into a small number of larger more cohesive commits. You can do this with an interactive rebase:

`# Rebase all commits on your development branch`

`git checkout`

`git rebase -i master`

This will open up a text editor where you can specify which commits to squash.

#### Submitting

After you committed and pushed all of your changes to GitHub, go to the page for your fork on GitHub, select your development branch, and click the pull request button. If you need to make any adjustments to your pull request, just push the updates to GitHub. Your pull request will automatically track the changes on your development branch and update.

#### Accepting and Merging a Pull Request

If the previous sections were written from the perspective of someone who created a fork and generated a pull request, this section is written from the perspective of the repository owner who deals with the incoming pull request. Thus, where the “forker” was referring to the original repository as upstream, we are now looking at it as the owner of that original repository and the standard origin remote.

#### Checking Out and Testing Pull Requests

Open up the `.git/config` file and add a new line under `[remote "origin"]`:

`fetch = +refs/pull/*/head:refs/pull/origin/*`

Now you can fetch and checkout any pull request so that you can test them:

`# Fetch all pull request branches`

`git fetch origin`

``

`​# Checkout out a given pull request branch based on its number`

`git checkout -b 999 pull/origin/999`

Keep in mind that these branches will be read-only and you won’t be able to push any changes.

#### Automatically Merging a Pull Request

In cases where the merge would be a simple fast-forward, you can automatically do the merge by just clicking the button on the pull request page on GitHub.

#### Manually Merging a Pull Request&#x20;

To do the merge manually, you will need to checkout the target branch in the source repo, pull directly from the fork, and then merge and push.

`# Checkout the branch you're merging to in the target repo`

`git checkout master`

``

`​# Pull the development branch from the forked repo where the pull request development was done.`

`git pull https://github.com/forkuser/forkedrepo.git newfeature​`

``

`# Merge the development branch`

`git merge newfeature​`

``

`# Push master with the new feature merged into it`

`git push origin master`

Now that you’re done with the development branch, you’re free to delete it.

`` `shell git branch -d newfeature` ``



**Copyright**

Copyright 2017, Chase Pettit

MIT License, [http://www.opensource.org/licenses/mit-license.php](https://opensource.org/licenses/mit-license.php)

**​Additional Reading**

​[Atlassian - Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

**​Sources​**

[GitHub - Fork a Repo​​](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

[GitHub - Syncing a Fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork)

[​​GitHub - Checking Out a Pull Request​](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/checking-out-pull-requests-locally)
