# git-flow (CJS Edition)

A collection of Git extensions to provide high-level repository operations
for Vincent Driessen's [branching model](http://nvie.com/git-model "original
blog post"). This fork adds functionality not added to the original branch.

## Why another git-flow fork
The last commit to [gitflow-avh](https://github.com/petervanderdoes/gitflow-avh)
was on May 23, 2019. Since then there have been a number of issues opened that have
not be resolved. This fork will address those outstanding issues and open PR's along
with continueing to maintain the git-flow branching model.

## Getting started

For the best introduction to get started with `git flow`, please read Jeff
Kreeftmeijer's blog post:

[Using git-flow to automate your git branching workflow](https://jeffkreeftmeijer.com/git-flow/)

Or have a look at one of these screen casts:

* [How to use a scalable Git branching model called git-flow](https://www.youtube.com/watch?v=-8DgENtFWSU) (by Build a Module)
* [A short introduction to git-flow](https://vimeo.com/16018419) (by Mark Derricutt)
* [On the path with git-flow](https://vimeo.com/37408017) (by Dave Bock)

A quick cheatsheet was made by Daniel Kummer:

[https://danielkummer.github.io/git-flow-cheatsheet/](https://danielkummer.github.io/git-flow-cheatsheet/)

## Installing git-flow

See the Wiki for up-to-date [Installation Instructions](https://github.com/CJ-Systems/gitflow-cjs/wiki/Installation).


## Integration with your shell

For those who use the [Bash](https://www.gnu.org/software/bash/) or [ZSH](https://www.zsh.org/)
shell, you can use my [fork of git-flow-completion](https://github.com/petervanderdoes/git-flow-completion)
which includes several additions for git-flow (AVH Edition), or you can use the
original [git-flow-completion](https://github.com/bobthecow/git-flow-completion)
project by [bobthecow](https://github.com/bobthecow). Both offer tab-completion
for git-flow subcommands and branch names with my fork including tab-completion
for the commands not found in the original git-flow.


## FAQ

* See the [FAQ](https://github.com/CJ-Systems/gitflow-cjs/wiki/FAQ) section
of the project Wiki.
* Version Numbering Scheme.  
Starting with version 1.0, the project uses the following scheme:
\<MAJOR\>.\<MINOR\>.\<REVISION\>\
* CJS is the acronym of "CJ Systems"

## Please help out

This project is under constant development. Feedback and suggestions are very
welcome and I encourage you to use the [Issues
list](https://github.com/CJ-Systems/gitflow-cjs/issues) on Github to provide that
feedback.

Feel free to fork this repository and to commit your additions. For a list of
all contributors, please see the [AUTHORS](AUTHORS) file.

Any questions, tips, or general discussion can be posted to the Google group:
[http://groups.google.com/group/gitflow-users](https://groups.google.com/g/gitflow-users)
This is the original group set up to support the nvie branch, but I am monitoring
the list as well for any questions related to my version.
When you do post a question on the list please indicate which version you are,
using the complete version number.

## Contributing

If you are resubmiting an open pull request see below. If submiting a new pull request addressing an already open issue with gitflow-avh please link the relevant issue in the description. For any new issues please see below

### Quick Start for new issues

* Please fork and clone a local copy of [gitflow-cjs](https://github.com/CJ-Systems/gitflow-cjs).
* Create a seperate issue branch based off develop.
* Commit commit you fix to the local branch.
* Please update your local copy with the latest devlop branch of [gitflow-cjs](https://github.com/CJ-Systems/gitflow-cjs)
* Rebase develop onto your local branch.
* Push your fix to your fork.
* When ready to submit a pull request.

### How to submit a pull request
When resubmitting an open pull request from [gitflow-avh](https://github.com/petervanderdoes/gitflow-avh) the base repository will need to be changed from petervanderdoes/gitflow-avh to CJ-Systems/gitflow-cjs.

For any new PRs releated to gitflow-cjs you can use on of the keywords from [Linking a pull request to an issue](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword) to automatically close the releated issue.

## License terms

git-flow is published under the FreeBSD License, see the
[LICENSE](LICENSE) file. Although the FreeBSD License does not require you to
share any modifications you make to the source code, you are very much
encouraged and invited to contribute back your modifications to the community,
preferably in a Github fork, of course.


## git flow usage

### Initialization

To initialize a new repo with the basic branch structure, use:

    git flow init [-d]

This will then interactively prompt you with some questions on which branches
you would like to use as development and production branches, and how you
would like your prefixes be named. You may simply press Return on any of
those questions to accept the (sane) default suggestions.

The ``-d`` flag will accept all defaults.

![Screencast git flow init](https://i.imgur.com/lFQbY5V.gif)

### Creating feature/release/hotfix/support branches

* To list/start/finish/delete feature branches, use:

```shell
git flow feature
git flow feature start <name> [<base>]
git flow feature finish <name>
git flow feature delete <name>
```

  For feature branches, the `<base>` arg must be a branch, when omitted it defaults to the develop branch.

* To push/pull a feature branch to the remote repository, use:

```shell
git flow feature publish <name>
git flow feature track <name>
```

* To list/start/finish/delete release branches, use:

```shell
git flow release
git flow release start <release> [<base>]
git flow release finish <release>
git flow release delete <release>
```

  For release branches, the `<base>` arg must be a branch, when omitted it defaults to the develop branch.

* To list/start/finish/delete hotfix branches, use:

```shell
git flow hotfix
git flow hotfix start <release> [<base>]
git flow hotfix finish <release>
git flow hotfix delete <release>
```

  For hotfix branches, the `<base>` arg must be a branch, when omitted it defaults to the production branch.

* To list/start support branches, use:

```shell
git flow support
git flow support start <release> <base>
```

  For support branches, the `<base>` arg must be a branch, when omitted it defaults to the production branch.

### Share features with others

You can easily publish a feature you are working on. The reason can be to allow other programmers to work on it or to access it from another machine. The publish/track feature of gitflow simplify the creation of a remote branch and its tracking.

When you want to publish a feature just use:
```shell
git flow feature publish <name>
```

or, if you already are into the `feature/<name>` branch, just issue:
```shell
git flow feature publish
```

Now if you execute `git branch -avv` you will see that your branch `feature/<name>` tracks `[origin/feature/<name>]`. To track the same remote branch in another clone of the same repository use:
```shell
git flow feature track <name>
```

This will create a local feature `feature/<name>` that tracks the same remote branch as the original one, that is `origin/feature/<name>`.

When one developer (depending on your work flow) finishes working on the feature he or she can issue `git flow feature finish <name>` and this will automatically delete the remote branch. All other developers shall then run:
```shell
    git flow feature delete <name>
```

to get rid of the local feature that tracks a remote branch that no more exist.

### Share hotfixes with others

You can publish an hotfix you are working on. The reason can be to allow other programmers to work on it or validate it or to access it from another machine.

When you want to publish an hotfix just use (as you did for features):
```shell
git flow hotfix publish <name>
```

or, if you already are into the `hotfix/<name>` branch, just issue:
```shell
git flow hotfix publish
```

Other developers can now update their repositories and checkout the hotfix:
```shell
git pull
git checkout hotfix/<name>
```
and eventually finish it:
```shell
git flow hotfix finish
```


### Using Hooks and Filters

For a wide variety of commands hooks or filters can be called before and after
the command.  
The files should be placed in .git/hooks  
In the directory hooks you can find examples of all the hooks available.


## Showing your appreciation

Of course, the best way to show your appreciation for the git-flow tool itself
remains contributing to the community.  If you'd like to show your appreciation
in another way, however, consider donating through PayPal:

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/donate/?hosted_button_id=GU25NCHMVMT9U)

