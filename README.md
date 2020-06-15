## Git-issues test

This repo is a simple experiment to test both:
* **git-issues** from https://github.com/duplys/git-issues ( my fixes - see below - in https://github.com/yorikvanhavre/git-issues ) - simple, no github integration, but coded in python
* **git-issue** from https://github.com/dspinellis/git-issue , more powerful, has github integration, coded in shellscript

The general idea is that your issues are stored together with the code, in the repository itself. Git-issues works by adding an "issues" branch to your repo, which in principle you never need to checkout yourself. That branch contains all the issues. Git-issue creates a .issues folder and stores the issues there.
 

## Install

### Linux

#### Git-issues

- Git clone the https://github.com/duplys/git-issues.git repo
- Make a symlink of **git-issues** to one of your exec paths, for ex. $USER/.local/bin
- Make a symlink of **gitshelve.py** either to the same dir as above, or to a python modules path

After that you can simply run **git issues** or **git-issues**

#### Git-issue

- Git clone the https://github.com/dspinellis/git-issue repo
- `sudo make install` (or follow local install procedure in readme)
- If you don't have vi installed (hardcoded in git-issue.. sigh...) symlink vi to any other text editor like nano, ne etc
- `apt-install jq` (json compiler)

## Usage

### git-issues

- **git issues** : Shows help text
- **git issues list** : lists issues
- **git issues new "My first issue"** : Creates an issue
- **git issues close 1** : Closes issue 1 (number obtained from `git issues list`) - Warning, it might be unsafe to refer to an issue by order number. Better to refer to it by its hash:
- **git issues close d703d01** : The better way
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

### git-issue

- **git issue** : Prints help text
- **git issue init** : Preares the repo for issues - needed before adding any new issue
- **echo .issues >> .gitignore** : After the stage above, an .issues folder is created, which is a git repo by itself, so it gets in conflict with your main repo's git system. So it should be added to the .gitignore of its host repo. git-issue actually wants you to either store the issues in another, separate repo than your main repo, or in the main repo, but in a separate branch, like git-issues (illustrated below)
- **git issue list** : Prints a list of issues
- **git issue new** or **git issue new -s "my first issue"** : Creates a new issue
- **git issue edit 172c132** : edits issue's title and desciption
- **git issue comment 172c132** : adds a comment
- **git issue show 172c132** or **git issue show -c 172c132** : Shows the issue (with comments)

Seeting everything up for sync:

- **git remote -v** : Shows the main URL of this repo (for the later step)
- **cd .issues**
- **git remote add origin git@github.com:yorikvanhavre/git-issues-test.git** : Create an origin remote and give it the same URL as our main one
- **git checkout -b issue** : Create a local branch with the same name you plan to use on remote server, in this case we create an "issue" branch (to not confound with the .issues branch I created above with git-issues). For git issue push to work correctly, both local/remote need the same name
- **git push -u origin issue** : specify which remote branch our .issues folder is associated to
- **cd ..**
- **git issue push** : To commit any new change
- **git issue pull** : To fetch any new changes
- **git issue exportall github yorikvanhavre git-issues-test** : *should* export/sync with github issues, but it gives me a github API communication failure

## Conclusion, which one?

Not sure yet. git-issue has more features, but it's much harder to fix problems. Once git-issue has been properly set up, which is a bit harder, both work pretty much the same way, by pushing/pulling to a branch. Github/gitlab integration is definitely a plus, but I couldn't make it work yet...

## TODO - git-issues fixes

Git-issues is easy to better. Improvements I see interesting:

- [x] In issues list, instead of showing order number starting from 1, use the stored index number
- [x] In issues list, show number of comments
- [x] In issues show, commets display is garbled

Done in https://github.com/yorikvanhavre/git-issues/commit/6f8089aa71b12693527227f394c7fd25f45134ff

- [ ] Add github integration (using python-github module?)
