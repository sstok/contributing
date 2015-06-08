Git Protocol
============

A guide for programming within version control.

Maintain a Repo
---------------

* Avoid including files in source control that are specific to your
  development machine or process.
* Delete local and remote feature branches after merging.
* Perform work in a feature branch.
* Use the rebase strategy when pulling in changes from a (remote) branch,
  to prevent creating merge-bubbles;
* Rebase frequently to incorporate upstream changes.
* Use a [pull request] for code reviews.
* User specific files should not appear in ``.gitignore``,
  use ``.git/info/exclude`` or [git global-ignore].
* Configure `.gitattributes` to ignore-export unneeded files and directories
  including docs, tests, notes and Git files them selves.
* Use [Gush] for merging pull requests.
* Avoid ``git push --force`` to a shared branch (like master).
* Avoid squashing commits with multiple authors (retain original authorship).
* Avoid running the CI checker when it is not needed (none functional changes).

[pull request]: https://help.github.com/articles/using-pull-requests/
[git global-ignore]: https://help.github.com/articles/ignoring-files/#create-a-global-gitignore
[Gush]: http://gushphp.org/

Setting up Gush
---------------

Gush automates common maintainer and contributor tasks.
Including the batch tagging of issues/pull request, merging pull requests with
complete details and updating the copyright header of source files.

Gush is written in PHP but can be used with any type of project or language.

To install Gush run the following command:

    curl -sS http://gushphp.org/installer | php`
    
Then configure it for future usage using:

    ./gush.phar core:configure
    
Make sure sure to configure the GitHub adapter when you want to
contribute to Rollerworks.
    
Write a Feature
---------------

Create a local feature branch based off master.

    git checkout master
    git pull --ff-only upstream master
    git checkout -b <branch-name>
    
*If you're not using a fork, prefix the branch name
with your initials.*

Rebase frequently to incorporate upstream changes.

    git fetch upstream
    git rebase upstream/master

Resolve conflicts. When the feature is complete and tests pass,
stage the changes.

    git add --all

When you've staged the changes, commit them.

    git status
    git commit --verbose

Write a [good commit message]. Example format:

    Present-tense summary under 50 characters

    * More information about commit (under 72 characters).
    * More information about commit (under 72 characters).

    http://project.management-system.com/ticket/123

If you've created more than one commit, use a rebase to squash them into
cohesive commits with good messages:

    git rebase -i upstream/master

Share your branch.

    git push origin <branch-name>

Submit a GitHub pull request with Gush:

    ./gush.phar pull:create

If you are using a fork, you need to use the following instead.

    ./gush.phar pull:create

Ask for a code review in the project's chat room.

If there is no chat room, wait till someones is available for the reviewing. 

[good commit message]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html

Review Code
-----------

A team member other than the author reviews the pull request. They follow
[Code Review](/code-review) guidelines to avoid miscommunication.

They make comments and ask questions directly on lines of code in the GitHub
web interface or in the project's chat room.

For changes which they can make themselves, they check out the branch.

    git checkout <branch-name>
    git diff staging/master..HEAD

They make small changes right in the branch, test the feature on their machine,
run tests, commit, and push.

When satisfied, they comment on the pull request `Ready to merge.`

Merge
-----

Rebase interactively. Squash commits like "Fix whitespace" into one or a
small number of valuable commit(s). Edit commit messages to reveal intent. Run
tests.

    git fetch upstream
    git rebase -i upstream/master

Force push your branch. This allows GitHub to automatically close your pull
request and mark it as merged when your commit(s) are pushed to master. It also
makes it possible to [find the pull request] that brought in your changes.

    git push --force origin <branch-name>

View a list of new commits. View changed files.

    git log origin/master..<branch-name>
    git diff --stat origin/master
    
* \<pr-number\> is number of the pull request
* \<pr-type\> is a single word, eg: feature, bug, minor, doc, style, security.
    
    ./gush.phar pull:merge <pr-nr> <pr-type>

Delete your remote feature branch.

    git push origin --delete <branch-name>

Delete your local feature branch.

    git branch --delete <branch-name>

[find the pull request]: http://stackoverflow.com/a/17819027
