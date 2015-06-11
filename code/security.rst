Security Issues
===============

.. note::

    Each Each project may follow a more detailed protocol for
    handling security issues. This document explains how security
    issues are handled (in general) by the core team.

Reporting a Security Issue
--------------------------

If you think that you have found a security issue in a project,
don't use the mailing-list or the bug tracker and don't publish it publicly.
Instead, all security issues must be sent to the private e-mail address
of the project's maintainer.

The project's maintainer can be found in the copyright header of source files.

Resolving Process
-----------------

For each report, we first try to confirm the vulnerability. When it is
confirmed, the core-team works on a solution following these steps:

#. Send an acknowledgement to the reporter;
#. Work on a patch;
#. Get a CVE identifier from mitre.org;
#. Write a security announcement for the projects website about the
   vulnerability. This post should contain the following information:

   * a title that always include the "Security release" string;
   * a description of the vulnerability;
   * the affected versions;
   * the possible exploits;
   * how to patch/upgrade/workaround affected applications;
   * the CVE identifier;
   * credits.
#. Send the patch and the announcement to the reporter for review;
#. Apply the patch to all maintained versions of the project;
#. Package new versions for all affected versions;
#. Publish the post on the official website;
#. Update the public `security advisories database`_ maintained by the
   FriendsOfPHP organization and which is used by the ``security:check`` command.

.. note::

    Releases that include security issues should not be done on Saturday or
    Sunday, except if the vulnerability has been publicly posted.

.. note::

    While we are working on a patch, please do not reveal the issue publicly.

.. note::

    The resolution takes anywhere between a couple of days to a month depending
    on its complexity.

.. _GitHub organization: https://github.com/rollerworks
.. _`security advisories database`: https://github.com/FriendsOfPHP/security-advisories
