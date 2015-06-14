Submitting a Patch
==================

Patches are the best way to provide a bug fix or to propose enhancements to
a project.

Step 1: Setup your Environment
------------------------------

Install the Software Stack
~~~~~~~~~~~~~~~~~~~~~~~~~~

Before working on a patch, setup a friendly environment with the following
software:

* Git 1.9.1 or above;
* PHP version 5.4 or above;
* PHPUnit 4.5.3 or above.

.. note::

    Some projects may require additional software, check the README.md file
    within in the root folder of the repository for specific requirements.

Configure Git
~~~~~~~~~~~~~

Set up your user information with your real name and a working email address:

.. code-block:: bash

    $ git config --global user.name "Your Name"
    $ git config --global user.email you@example.com

.. tip::

    If you are new to Git, you are highly recommended to read the excellent and
    free `ProGit`_ book.

.. tip::

    If your IDE creates configuration files inside the project's directory,
    you can use global ``.gitignore`` file (for all projects) or
    ``.git/info/exclude`` file (per project) to ignore them. See
    `GitHub's documentation`_.

.. tip::

    Windows users: when installing Git, the installer will ask what to do with
    line endings, and suggests replacing all LF with CRLF. This is the wrong
    setting if you wish to contribute! Selecting the as-is method is
    your best choice, as Git will convert your line feeds to the ones in the
    repository. If you have already installed Git, you can check the value of
    this setting by typing:

    .. code-block:: bash

        $ git config core.autocrlf

    This will return either "false", "input" or "true"; "true" and "false" being
    the wrong values. Change it to "input" by typing:

    .. code-block:: bash

        $ git config --global core.autocrlf input

    Replace --global by --local if you want to set it only for the active
    repository

Setting up Gush
~~~~~~~~~~~~~~~

To make contributing as simple as possible it's recommended to use `Gush`_
for opening pull-request, forking repositories and taking issues.

.. ::

    If you would rather use only Git this is also possible, but will require a bit
    more work. The rest of this document uses Gush, see :doc:`patches_with_git <Submitting a Patch with Git>`
    if you only want to use Git.

To install Gush read all the details at: TBD.

Once you have installed Gush you must configure it for future usage:

.. code-block:: bash

    $ gush core:configure

Make sure sure to configure the GitHub adapter.
That's it, you are now ready to use Gush.

    .. note::

        The GitHub adapter requires that you have a `GitHub`_, if don't
        have an account already then sign-up first (it's free).

Get the Project Source Code
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Get the Project source code:

* Fork the "Project repository" and clone your fork locally
  (this will create a ``project-name`` directory, like: symfony):

.. code-block:: bash

      $ gush branch:fork YOUR-USERNAME PROJECT-NAME

Replace ORGANIZATION with the organization name of the repository (like rollerworks)
and PROJECT-NAME with the repository name (like: search).

Gush has forked the organization's repository into your GitHub account
and cloned (the forked) repository to your system.

.. note::

    Whenever you want to use Gush for a project you must be in the local
    repository folder.

Check that the current Tests Pass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now that the code is installed, check that all unit tests pass for your
environment as explained in the 'Tests' section of the projects README.md file.

Step 2: Work on your Patch
--------------------------

The License
~~~~~~~~~~~

Before you start, you must know that all the patches you are going to submit
must be released under the *MIT license*, unless explicitly specified in your
commits.

Choose the right Branch
~~~~~~~~~~~~~~~~~~~~~~~

Before working on a patch, you must determine on which branch you need to
work. The branch should be based on the ``master`` branch if you want to add a
new feature. But if you want to fix a bug, use the oldest but still maintained
version of the project where the bug happens (like ``1.0``).

.. note::

    All bug fixes merged into maintenance branches are also merged into more
    recent branches on a regular basis. For instance, if you submit a patch
    for the ``1.0`` branch, the patch will also be applied by the core team on
    the ``master`` branch.

Create a Topic Branch
~~~~~~~~~~~~~~~~~~~~~

Each time you want to work on a patch for a bug or on an enhancement, create a
topic branch:

.. code-block:: bash

    $ git checkout -b BRANCH_NAME master

Or, if you want to provide a bugfix for the ``1.0`` branch, first track the remote
``1.0`` branch locally:

.. code-block:: bash

    $ git checkout -t origin/1.0

Then create a new branch off the ``1.0`` branch to work on the bugfix:

.. code-block:: bash

    $ git checkout -b BRANCH_NAME 1.0

.. tip::

    If you want work an existing issue use the following command instead:

    .. code-block:: bash

        $ gush issue:take 1111 --base=1.0

    And replace 1111 with the actual issue-number.

The above checkout commands automatically switch the code to the newly created
branch (check the branch you are working on with ``git branch``).

Work on your Patch
~~~~~~~~~~~~~~~~~~

Work on the code as much as you want and commit as much as you want; but keep
in mind the following:

* Read about the code :doc:`conventions <conventions>` and follow the
  coding :doc:`standards <standards>` (use ``git diff --check`` to check for
  trailing spaces -- also read the tip below);

* Add unit tests to prove that the bug is fixed or that the new feature
  actually works;

* Try hard to not break backward compatibility (if you must do so, try to
  provide a compatibility layer to support the old way) -- patches that break
  backward compatibility have less chance to be merged;

* Do atomic and logically separate commits (use the power of ``git rebase`` to
  have a clean and logical history);

* Squash irrelevant commits that are just about fixing coding standards or
  fixing typos in your own code;

* Never fix coding standards in some existing code as it makes the code review
  more difficult;

* Write good commit messages (see the tip below).

.. tip::

    When submitting pull requests, `StyleCI`_ verifies that you are using
    the PHP coding standards as defined in `PSR-1`_ and `PSR-2`_.

    A status is posted below the pull request description with a summary
    of any problems it detects or any Travis CI build failures.

.. tip::

    A good commit message is composed of a summary (the first line),
    optionally followed by a blank line and a more detailed description. The
    summary should start with the Component you are working on in square
    brackets (``[DependencyInjection]``, ``[FrameworkBundle]``, ...).

    Use clear and descriptive commit messages in the present tense,
    “change” not “changed” or “changes” to start the summary and don't
    add a period at the end.

    Using "and" in the first line, is a a good indication your commit is not
    atomic. Try to split the commit with ``git rebase``.

    See also: `A Note About Git Commit Messages`_ for more tips.

Prepare your Patch for Submission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When your patch is not about a bug fix (when you add a new feature or change
an existing one for instance), it must also include the following:

* An explanation of the changes in the relevant ``CHANGELOG`` file(s) (the
  ``[BC BREAK]`` or the ``[DEPRECATION]`` prefix must be used when relevant);

* An explanation on how to upgrade an existing application in the relevant
  ``UPGRADE`` file(s) if the changes break backward compatibility or if you
  deprecate something that will ultimately break backward compatibility.

Step 3: Submit your Patch
-------------------------

Whenever you feel that your patch is ready for submission, follow the
following steps.

Rebase your Patch
~~~~~~~~~~~~~~~~~

Before submitting your patch, update your branch (needed if it takes you a
while to finish your changes):

.. code-block:: bash

    $ git fetch upstream
    $ git rebase upstream/master

.. tip::

    Replace ``master`` with the branch you selected previously (e.g. ``1.0``)
    if you are working on a bugfix.

.. ::

    There is a pending feature request for Gush that will make updating
    your patch (pull request) much easier).

    https://github.com/gushphp/gush/issues/410

When doing the ``rebase`` command, you might have to fix merge conflicts.
``git status`` will show you the *unmerged* files. Resolve all the conflicts,
then continue the rebase:

.. code-block:: bash

    $ git add ... # add resolved files
    $ git rebase --continue

Check that all tests still pass and push your branch remotely:

.. code-block:: bash

    $ gush branch:push --force

Make a Pull Request
~~~~~~~~~~~~~~~~~~~

You can now make a pull request on the GitHub repository.

To ease the core team work, always include the modified components in your
pull request message, like in:

.. code-block:: text

    [Yaml] fix something
    [Form] [Validator] [FrameworkBundle] add something

The pull request description (not the commit message) must include the
following checklist at the top to ensure that contributions may be reviewed
without needless feedback loops and that your contributions can be included
as quickly as possible:

.. code-block:: text

    | Q             | A
    | ------------- | ---
    | Bug fix?      | [yes|no]
    | New feature?  | [yes|no]
    | BC breaks?    | [yes|no]
    | Deprecations? | [yes|no]
    | Tests pass?   | [yes|no]
    | Fixed tickets | [comma separated list of tickets fixed by the PR]
    | License       | MIT
    | Doc PR        | [The reference to the documentation PR if any]

An example submission could now look as follows:

.. code-block:: text

    | Q             | A
    | ------------- | ---
    | Bug fix?      | no
    | New feature?  | no
    | BC breaks?    | no
    | Deprecations? | no
    | Tests pass?   | yes
    | Fixed tickets | #12, #43
    | License       | MIT
    | Doc PR        | organization/project-docs#123

.. tip::

    Gush will automatically create in the description table for you,
    all you must do is provide the answer for each question.

Some answers to the questions trigger some more requirements:

* If you answer yes to "Bug fix?", check if the bug is already listed in the
  issues and reference it/them in "Fixed tickets";

* If you answer yes to "New feature?", you must submit a pull request to the
  documentation and reference it under the "Doc PR" section; (only certain projects)

* If you answer yes to "BC breaks?", the patch must contain updates to the
  relevant ``CHANGELOG`` and ``UPGRADE`` files;

* If you answer yes to "Deprecations?", the patch must contain updates to the
  relevant ``CHANGELOG`` and ``UPGRADE`` files;

* If the "license" is not MIT, just don't submit the pull request as it won't
  be accepted anyway.

If some of the previous requirements are not met, create a todo-list and add
relevant items:

.. code-block:: text

    - [ ] fix the tests as they have not been updated yet
    - [ ] submit changes to the documentation
    - [ ] document the BC breaks

If the code is not finished yet because you don't have time to finish it or
because you want early feedback on your work, add an item to todo-list:

.. code-block:: text

    - [ ] finish the code
    - [ ] gather feedback for my changes

As long as you have items in the todo-list, please prefix the pull request
title with "[WIP]".

In the pull request description, give as much details as possible about your
changes (don't hesitate to give code examples to illustrate your points). If
your pull request is about adding a new feature or modifying an existing one,
explain the rationale for the changes. The pull request description helps the
code review and it serves as a reference when the code is merged (the pull
request description and all its associated comments are part of the merge
commit message).

.. tip::

    Gush allows to use an external editor for big descriptions
    but doesn't support adding images.

    After the pull request is created you can always change the description
    using the GitHub web application to add additional information.

In addition to this "code" pull request, you may also send a pull request to
the documentation repository to update the documentation when appropriate.

Rework your Patch
~~~~~~~~~~~~~~~~~

Based on the feedback on the pull request, you might need to rework your
patch. Before re-submitting the patch, rebase with ``upstream/master`` or
``upstream/1.0``, don't merge; and force the push to the origin:

.. code-block:: bash

    $ git rebase -f upstream/master
    $ gush branch:push --force

.. ::

    There is a pending feature request for Gush that will make updating
    your patch (pull request) much easier).

    https://github.com/gushphp/gush/issues/410

Often, moderators will ask you to "squash" your commits. This means you will
convert many commits to one commit. To do this, use the rebase command:

.. code-block:: bash

    $ git rebase -i upstream/master
    $ gush branch:push --force

.. caution::

    Make sure you don't have any remote changes that are not in
    your local branch! When you are not sure update you local branch is
    up-to-date run the following commands:

    .. code-block:: bash

        $ git fetch origin
        $ git rebase origin/BRANCH-NAME

After you type this command, an editor will popup showing a list of commits:

.. code-block:: text

    pick 1a31be6 first commit
    pick 7fc64b4 second commit
    pick 7d33018 third commit

To squash all commits into the first one, remove the word ``pick`` before the
second and the last commits, and replace it by the word ``squash`` or just
``s``. When you save, Git will start rebasing, and if successful, will ask
you to edit the commit message, which by default is a listing of the commit
messages of all the commits. When you are finished, execute the push command.

.. tip::

    If you need to squash "all" the commit messages, simple use the
    following command instead.

    .. code-block:: bash

        $ gush pull-request:squash --force 111

    And replace 111 with the actual pull request number.

.. _ProGit:                                http://git-scm.com/book
.. _GitHub:                                https://github.com/signup/free
.. _`GitHub's Documentation`:              https://help.github.com/articles/ignoring-files
.. _`Gush`:                                http://gushphp.org/
.. _`StyleCI`:                             https://styleci.io/
.. _travis-ci.org:                         https://travis-ci.org/
.. _`travis-ci.org status icon`:           http://about.travis-ci.org/docs/user/status-images/
.. _`travis-ci.org Getting Started Guide`: http://about.travis-ci.org/docs/user/getting-started/
.. _`PSR-1`:                               http://www.php-fig.org/psr/psr-1/
.. _`PSR-2`:                               http://www.php-fig.org/psr/psr-2/
.. _`A Note About Git Commit Messages`:    http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
