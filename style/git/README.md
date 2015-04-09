Git
===

* Write a [good commit message].
* Use clear and descriptive commit messages in the present tense,
   “change” not “changed” or “changes”;
* Squash multiple trivial commits into a single commit.
* Avoid merge commits by using a [rebase workflow].
* Avoid adding a date or planned release version in the branch names.
* Prefix a branch a logical type like: bug, feature or minor (none functional changes).

[rebase workflow]: /protocol/git#merge
[good commit message]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
   
Pull Requests
-------------

* A pull request who is not ready for merging must begin with `[WIP]`
  in the pull request title;
* Each pull request must have a short summary describing some of the most
  important details.
* Each pull-request must be small and precise, avoid adding unrelated changes in files
  or code. Including: style changes, removing dead code, rearranging methods, etc.

```markdown
| Q             | A
| ------------- | ---
| Bug fix       | [yes|no]
| New feature   | [yes|no]
| BC breaks     | [yes|no]
| Deprecations  | [yes|no]
| Tests pass    | [yes|no]
| Fixes         | [comma separated list of tickets fixed by the PR]
```

For example:

```markdown
    | Q             | A
    | ------------- | ---
    | Bug fix       | no
    | New feature   | no
    | BC breaks     | no
    | Deprecation   | no
    | Tests pass    | yes
    | Fixed         | #12, #43, #100
```

If the pull-request is tested automatically using a continues
integration system then the `Tests pass` can be omitted.

Public repository
-----------------

A public repository is viewable by any person,
and accepts pull requests for from any person or organization.

...

Private repository
------------------

A private repository has limited access, and is only viewable
by organization team members.

* Private repositories should not use forks.
* Prefix feature branch names with your initials (username).

...
