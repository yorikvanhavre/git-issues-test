## Git-issues test

This repo is a simple experiment to test git-issues from https://github.com/duplys/git-issues ( my fixes - see below - in https://github.com/yorikvanhavre/git-issues )

The general idea is that your issues are stored together with the code, in the repository itself. It works by adding an "issues" branch to your repo, which in principle you never need to checkout yourself. That branch contains all the issues.

There is also "git-issue" at https://github.com/dspinellis/git-issue which has more powers,but this one being coded in python, it is easy to hack...

## Install

### Linux

- Git clone the https://github.com/duplys/git-issues.git repo
- Make a symlink of **git-issues** to one of your exec paths, for ex. $USER/.local/bin
- Make a symlink of **gitshelve.py** either to the same dir as above, or to a python modules path

After that you can simply run **git issues** or **git-issues**

## Usage

- **git issues** : Shows help text
- **git issues list** : lists issues
- **git issues new "My first issue"** : Creates an issue
- **git issues close 1** : Closes issue 1 (number obtained from `git issues list`) - Warning, after closing issue 1, issue 2 will appear as issue 1 in the list. It is unsafe to refer to an issue by order number. Better to refer to it by its hash:
- **git issues close d703d01** : The correct way
- **git issues show d703d01** : Shows details fo an issue
- **git issues change d703d01 severity minor** : Changes one attribute of the issue (see available attributes below)
- **git issues edit d703d01 severity** : Same thing but opens an editor
- **git issues comment 34c6f58 "Well done, this is a very interesting first issue"** : Adds a comment

Available attributes:

- title
- summary
- description
- author
- reporters
- owners
- assigned
- carbons
- issue_type
- status
- resolution
- components
- version
- milestone
- severity
- priority
- tags
- modified

## TODO - fixes

The code is a bit crappy but it's a python script, easy to better. Improvements I see interesting:

- In issues list, instead of showing order number starting from 1, use the stored index number https://github.com/duplys/git-issues/blob/master/git-issues#L1108
- In issues list, show number of comments
- In issues show, commets display is garbled
