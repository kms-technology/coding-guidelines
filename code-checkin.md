# KMS Code Check-in Standards

- [1. Purpose](#1-purpose)
- [2. Common Convention & Best Practices](#2-common-convention-best-practices)
    - [2.1. Practice 1: Commit only compliable code](#21-practice-1-commit-only-compliable-code)
    - [2.2. Practice 2: Don't commit user-settings and generated files](#22-practice-2-don't-commit-user-settings-and-generated-files)
    - [2.3. Practice 3: Never overwritten other's code](#23-practice-3-never-overwritten-other's-code)
    - [2.4. Practice 4: Blank comment is not accepted](#23-practice-4-blank-comment-is-not-accepted)
    - [2.5. Practice 5: Don't commit multiple purposes of changes once](#23-practice-5-don't-commit-multiple-purposes-of-changes-once)
    - [2.6. Practice 6: Commit single purpose of changes once](#23-practice-6-commit-single-purpose-of-changes-once)
- [3. Git Code Check-In Practices](#3-git-code-check-in-practices)
    - [3.1. Practice 1: Do not check-in large files](#31-practice-1-do-not-check-in-large-files)
    - [3.2. Practice 2: Configure line ending before doing check-in](#32-practice-2-configure-line-ending-before-doing-check-in)
    - [3.3. Practice 3: Merge code with right method](#33-practice-3-merge-code-with-right-method)
    - [3.4. Practice 4: Use Tag on releasing check-in](#34-practice-4-use-tag-on-releasing-check-in)

## 1. Purpose

This document describes a collection of standards, conventions, and guidelines for committing code to source control including SVN, Git. They are compiled from KMS developer own experiences and sound, proven best practices in the software development industry. 

## 2. Common Convention & Best Practices

### 2.1. Practice 1: Commit only compliable code

Project files, adding files/folders are often candidates for this mistake. Pay close attention on those files to avoid violating this rule.
If the project applies unit test, the committing code must passes all tests.

### 2.2. Practice 2: Don't commit user-settings and generated files

Those files are generated automatically by IDE tools (i.e. *.suo, .user, .metadata files) or development platform (i.e. .DS_Store file in Mac OS, node_modules folder of nodejs, etc.). As its content is specific for each individual workstation so don't bother others with your own settings by committing them.
Changes in configuration files (i.e. Web.config, App.config, etc...) for your own purpose also shouldn't be committed

To permanently ignore kind of files / folders:

* In Git, use .gitignore file. Read more at https://help.github.com/articles/ignoring-files
* In SVN, use svn:ignore property. Read more at http://tortoisesvn.net/docs/release/TortoiseSVN_en/tsvn-dug-ignore.html

### 2.3. Practice 3: Never overwritten other's code

This is a very basic rule but it is the most annoying thing when issue occurs. Good practice is do comparing changes between committing code and the current version for every file before submitting code. Version Control clients like TortoiseSVN and TortoiseGit support just one right-click to show two panels with changes are highlighted. 

### 2.4. Practice 4: Blank comment is not accepted

Never leave comment blank when committing your code. Comment what changes are for not what changes are.

For example, should log "RMGW01 - Login Use Case", "Ticket #4" instead of "Created login provider xyz" or "Added method Abc() to handler exception".

Including ticket number, bug number, feature name, UC, etc... in the comment is one of the best practices. For example, use "re #4" to link your commit to ticket #4. "references", "refs" and "see" will add a comment to the target ticket. Use "closes #4" to close ticket 4. "closed", "close", "fix", "fixed", and "fixes" will also close a ticket. Use "test #4" to move a ticket to "ready for test" status. 

With proper comments plus ShowLog feature in SVN or Git, tracing back changes has never been easier.

### 2.5	Practice 5: Don't commit multiple purposes of changes once

Avoid committing multiple changes into one single Changeset as this would be so hard to distinguish them later. Each time you commit your code, SVN/Git will increase the revision number. Revision number in SVN is similar to label in VSS or tag in CVS. If you pack many purposes of changes in one revision, you likely close your door to roll each individual change back. For example, you have fixed two tickets #1 and #2 and committed them by one Changeset. Later on, there is a request to roll back the fixing of ticket #1, how would you handle this situation?

### 2.6	Practice 6: Commit single purpose of changes once

Avoid dividing a single change into to multiple Changesets to commit, pack them on one Changeset if possible. For example, committing three Changesets for one bug fixing is not a good practice. SVN is a versioning tool not a backup place where developers submit code just because they are afraid of losing their effort when their computer crash. Committing your changes one time is extremely helpful for performing review code as it is easy to localize and locate changes in one revision (using ShowLog feature). It has never been easy when changes sit on multiple revisions.

## 3. Git Code Check-In Practices

### 3.1 Practice 1: Do not check-in large files

When it needs to include large files (10MB or more) to Git repository, consider alternative storage solutions for those and don’t add them to Git. Once these files were added to repository, anyone cloning it into their local box will waste their time for long downloading time and it’s not easy to remove them. Alternative storage solution could be putting them on file server and manually download them

### 3.2 Practice 2: Configure line ending before doing check-in

Due to historical reason, the line ending character in text document is different in Windows (\r\n) and Linux (\n). If a file is saved in Linux and then it is saved again in Windows without adding anything else, Git will include that file in new commit but the content is still unchanged except line ending characters. Git addressed this issue in its configuration but unfortunately it isn’t done automatically. Developers are responsible for configuring Git on their development box before checking in anything. Read more at https://help.github.com/articles/dealing-with-line-endings#platform-all

### 3.3 Practice 3: Merge code with right method

Git offers two methods for merging branches (e.g. local and remote branch): merging and rebasing. Whatever method is used, it results at least one new commits in history tree. Therefore, using incorrect merging method overtime creates unnecessary commits to history tree which causes developers / maintainers a lot of trouble on managing source code history. Developers are responsible for understanding well both of two merging methods and use them appropriately. Read more at http://blogs.atlassian.com/2013/10/git-team-workflows-merge-or-rebase

### 3.4 Practice 4: Use Tag on releasing check-in

Git’s Tag feature is dead simple but really helpful to mark a milestone on the history tree of source code e.g. for 2.0 release. A recommended practice is that every time the product goes into important milestone such as beta release or RTM build, a git tag should be created on the appropriate check-in for later on

