Git
===





This document explains some conventions and specificities in the way we manage
the projects code with Git.

.. tip::

    Most of our daily Git workflow is handled using `Gush`_.
    If you haven't used Gush before we know you will love it.

    See the subsection below for more information.

* Don't including files in source control that are specific to your
  development machine or process.
* Perform work in a feature/bug-fix branch.
* Use the rebase strategy when pulling in changes from a (remote) branch,
  to prevent creating merge-bubbles;
* Rebase frequently to incorporate upstream changes.
* User specific files should not appear in ``.gitignore``,
  use ``.git/info/exclude`` or `git global-ignore`_.
* Avoid squashing commits with multiple authors (retain original authorship).
* Avoid running the CI checker when this is not needed (none functional changes).
    * Add ``[skip ci]`` to commit message.
* Try to limit to the first line of the commit message (the subject) to 50 chars.

Gush
----

Gush automates common maintainer and contributor tasks.
Including the batch tagging of issues/pull-request, creating/updating and merging
pull requests (with complete details) and much more.

Gush is written in PHP but can be used with any type of project or language.

For more information on installing see the `Gush <Gush website>`_

Once you have installed Gush you must configure it for future
usage using::

    gush core:configure

Make sure sure to configure the GitHub adapter when you want to
contribute to Rollerworks.

Executing a Gush command should be done from your local git repository.

Forking the repository
~~~~~~~~~~~~~~~~~~~~~~

In order to the



Creating a pull request
~~~~~~~~~~~~~~~~~~~~~~~

TBD.

Taking an existing issue
~~~~~~~~~~~~~~~~~~~~~~~~

If you find a ticket/issue you would like to work on (remember we love contributors),
then please first inform others you will "take" the issue. Just post a simple reply like
"Seems simple enough, I will take a stab at this."

Then from your local repository execute the following command::

    gush issue:take 111

111 is the issue-id you want to take, that's it! Gush checkouted a new branch
for you starting working in.

Once you are happy with your changes execute::

    gush pull-request:create

To open a new pull-request, *don't worry if you forgot to push as Gush this will
do this automatically for you.*

Now wait for someone to do a review of your pull-request. If everything
is ok one of our team members will merge the pull-request.

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

.. _`pull request`: https://help.github.com/articles/using-pull-requests/
.. _`git global-ignore`: https://help.github.com/articles/ignoring-files/#create-a-global-gitignore
.. _`Gush`: http://gushphp.org/
