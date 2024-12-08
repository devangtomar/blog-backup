---
title: "Git commands you must unquestionably know! 🚀"
datePublished: Sat Aug 27 2022 16:49:09 GMT+0000 (Coordinated Universal Time)
cuid: cl7c6fjz708qi9ynv01zr357g
slug: git-commands-you-must-unquestionably-know-69aeb8594bd3
canonical: https://medium.com/@devangtomar123/git-commands-you-must-unquestionably-know-69aeb8594bd3
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1661621317379/6PoSfeSTI.jpeg
tags: linux, github, git, command-line, devops

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621294903/HzFNA11Kt.jpeg align="left")

The most widely used distributed version control system worldwide is called Git. This programme was developed back in 2005 by Linus Torvalds, the man responsible for the Linux kernel, and it is still an active open-source project today. Git is used for version control in countless open-source and for-profit projects.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621296468/kfj5m7RjR.jpeg align="left")

If you work in an IT-related sector, you must be highly familiar with Git. I’ll talk about some of the often used commands in this blog. This post will go over various Git commands that any developer, data scientist, or product manager should be familiar with.

### **Inspecting stuff 🕵️**

Let’s first have a look at inspecting changes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621299188/7L2KgfSke.gif align="left")

#### git diff

View all local file modifications. If you just want to see updates for one file, you can append the file name.

git diff

Some more examples :

> `*git diff filename*` *: For a Filename*

> `*git diff HEAD*` *: From last commit*

> `*git diff HEAD filename*` *: From last commit, for a specific file*

> `*git diff --staged HEAD*` *: From staging area*

> `*git diff --staged HEAD filename*` *: From staging area but for a specific file*

> `*git diff firstCommitID secondCommitID*` *: Between 2 commits*

> `*git diff HEAD HEAD^*` *: Between last commit and HEAD*

#### **git log**

See all commit history. Can also be used for a file with `git log -p my_file`. Enter `q` to exit. 📓

`git log`

Some more examples :`git log` : Checking previous commits logs etc

* `git log --all --oneline --decorate --graph` : For getting graph of git history
    
* `git log -- filename` : For checking git history of a file
    

#### git reflog

Git uses a feature known as reference logs, or “reflogs,” to keep track of alterations to the tips of branches. Many Git commands allow you to specify a reference, also known as “ref,” which is a pointer to a commit, as an argument.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621301034/VZO78z_xo.jpeg align="left")

Show a log of changes to the local repository’s HEAD. Good for finding lost work. 🔎

`git reflog`

Some more examples :

> `*git reflog show HEAD*` *: Show reflog for HEAD*

#### git blame

The git blame command is a flexible debugging tool with a wide range of application possibilities. The display of author metadata associated with specific committed lines in a file is the high-level function of git blame.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621302401/JIlzmH42f.jpeg align="left")

This is done in order to look over certain portions of a file’s history and determine who the most recent author who edited a line was. This is employed to investigate the past of certain code and provide answers to inquiries regarding the what, how, and why the code was added to a repository.

`git blame README.md`

Some more examples :

> `*git blame -L 1,6 sample.txt*` *:* The `-L` option will restrict the output to the requested line range. Here we have restricted the output to lines 1 through 6.

### Organising stuff 📚

Consider the following scenario: you are called to examine a production event, and after some research, you locate the commit that contains the problematic code.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621304420/iueMiTlQn.jpeg align="left")

Unfortunately, this results in the introduction of a new bug. It turns out that there was some code dependent on by another section of the app hidden in that old “broken” commit, and when you reversed those lines, it left the site once more in a broken state. I’m sorry.

How can circumstances like these be prevented? We must first look at the process through which these kinds of commits are created in order to provide a solution.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621306305/ySWBDnIAM.png align="left")

#### git commit amend

Your staged changes should be added to the most recent commit.  
This command only allows you to edit the most recent commit message if nothing is staged.

`git commit --amend -m "an updated commit message"`

> **Note :** Use this command only if the remote master branch hasn’t yet merged the commit! ⚠️

#### git push remote — tags

Like the majority of VCSs, Git enables users to mark particular moments in a repository’s history as being significant.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621308064/AlI8byRd4.jpeg align="left")

Typically, people employ this feature to indicate release points (v1.0, v2.0 and so on).

`git commit --amend -m "an updated commit message"`

Some more examples :

> `*git tag --list*` : For listing all tags

> `*git tag --delete tagName*` : For deleting specific tag

> `*git tag -a v.1.0*` and `*git show v.1.0*` : For annotated tag and showing it

> `*git diff v1.0.1 v1.0.2*` : Compare tags

> `*git tag -a beta.0.0.9 commitID*` : Add a tag to specific commit

> `*git tag -a beta.0.0.9 -f commitID*` : Update tag forcefully

### Reversing Actions 🔙

To reverse the consequences of repository changes, use git reset, git checkout, and git revert. It can be challenging to follow these instructions.  
You can use git reset and git checkout on both commits and specific files.  
Only at the commit level does git revert get used.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621309715/sivOKlN8W.jpeg align="left")

#### git reset — hard HEAD

Changes that have been staged or not since the last commit should be discarded. Git reset adjusts the staged snapshot to match the version from the supplied commit when it is called with a file path.

```yaml
git reset HEAD~2 sample.txt
```

Some more examples :

> `*git reset --soft commitID*` : Revert to a specific commit.. all new changes move to staging area

> `*git reset commitID*` : Revert to a specific commit.. all new changes will move to working area

> `*git reset --hard commitID*` : Revert to a specific commit.. all new changes erased \[No data recovery\]

#### git checkout commitName

Checkout works best for undoing local changes. It doesn’t muck up a remote branch’s commit history that your collaborators rely on!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621311927/icNHu340d.png align="left")

Instead of committing, you can use checkout with a branch, which updates the working directory and switches HEAD to the provided branch. The checkout command is most frequently used in this manner.

`git checkout c1e8fb5`

Some more examples :

> `*git checkout -b branchname*` : To create a new branch and switch to it in 1-go

#### git revert commitName

Although the git reverse command can be categorised as a “undo” command, it is not a conventional undo operation.

It determines how to reverse the modifications made by the commit and adds a new commit with the resulting inverted content rather than removing the commit from the project history. Due to the integrity of your revision history and the need for trustworthy collaboration, this keeps Git from losing its history.

`git revert c1e8fb5`

Some more examples :

> `git revert HEAD filename` : For reverting commit for a particular file

> `git revert HEAD~` : For any recent commit changes

### Make aliases for most used Git Commands ⏩

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621314139/yb0ab6KOM.jpeg align="left")

The following aliases can be added to your Bash terminal on macOS to generate shortcuts for Git commands

**Filename** : *.bash\_profile*

`alias gs='git status ' alias ga='git add ' alias gaa='git add -A ' alias gb='git branch ' alias gc='git commit ' alias gcm='git commit -m ' alias go='git checkout '`

The aforementioned can be modified to provide shortcuts for any Git commands you desire.  
If you don’t already have one, you can create one on macOS using the steps below:

`touch ~/.bash_profile`

and then open it with:

`open ~/.bash_profile`

See more info on *.bash\_profile* [here](https://stackoverflow.com/a/30462883/4590385).

Now, entering gs on your terminal is equivalent to entering git status. Please take note that after your shortcut, you can insert other flags in your terminal.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621315716/r03k0rwnP.jpeg align="left")

Git aliases are another option, but they require that you type git before the shortcut command. Still writing whole git commands? 😉

### Github URL for this article 💻

[**learning-devops-masterclass/git-tutorial.md at main · devangtomar/learning-devops-masterclass**  
\*Git commands : git init : For initializing any directory with git in it git clone repo-url : For cloning a repo git…\*github.com](https://github.com/devangtomar/learning-devops-masterclass/blob/main/git/git-tutorial.md)

### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on [Dev.to](http://Dev.to): [devangtomar](https://dev.to/devangtomar)