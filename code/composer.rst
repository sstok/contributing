Composer
========

Composer is a tool for dependency management in PHP.
It allows you to declare the dependent libraries your project needs and
it will install them in your project for you.

For more information visit :link:`https://getcomposer.org/`

.. note::

    We care gratefully for security, which is why it's recommend
    to always verify the Composer archive you downloaded.

    *Instructions for this are currently missing.*

    When you use ``composer self-update`` this should
    be done automatically already, only the "initial" download
    should be verified.

Best Practices
--------------

* Regularly update your local Composer installation.
* Specify the PHP version to be used on the project in the composer.json
    * Try to avoid using the newest version, PHP 5.6 is acceptable.
* Specify the PHP extensions to be used on the project in the composer.json
  like ``"ext-pgsql: "*"``.
* Specify the PHP version and extensions as minimum, don't specify a maximum
  PHP version (unless a new major version is incompatible).
* Avoid specifying version bounds without a limit like `>=2.0`
* Always include a license, type and description.
* Include a link to the contributes list.
* Don't add PHPUnit or tools (like php-cs-fixer) as a dev-requirement
  but use the Phar archive instead.
* Avoid using to restrictive version constraints (see the subsection below).
* Always use a secure connection for downloading Composer, package information
  and the actual package source. Never downgrade to plain HTTP!!,
  If TLS is not available then fix this, you can't trust a package that is
  not provided over a secure connection.
* Use ``composer require package-name`` or ``composer --dev require package-name`` (for dev requirements)
  to get the best available version.

``composer.json`` example:

.. note::

    The composer.json is in the JSON format, you can't leave
    any trailing spaces or comments.

    Always use ```composer validate`` to check if the file is properly formatted.

.. code-block:: json

{
    "name": "vendor-name/project-name",
    "description": "Short description",
    "keywords": ["one", or more", "keywords", "don't the project name itself"],
    "type": "project",
    "license": "MIT",
    "authors": [
        {
            "name": "Your name",
            "email": "your-email@addess.ext"
        },
        {
            "name": "Community contributions",
            "homepage": "https://github.com/vendor-name/project-name/contributors"
        }
    ],
    "require": {
        "php": ">=5.5",
    },
    "autoload": {
        "psr-4": {
            "ProjectVendor\\": ["src/"]
        }
    },
    "autoload-dev": {
        "psr-4": {
            "ProjectVendor\\Tests": ["tests/"]
        }
    }
}

Restrictive version constraints
-------------------------------

.. note::

    The practice described below is best applied when the
    required package(s) follow `Semantic versioning`_.

    In short Semantic version requires that breaking backward
    compatibility requires a major version bump (1.5 -> 2.0).

When you require a package in Composer you'd properly want to get
the latest available version with bug fixes and possible new features.

But not all changes may be compatible with your current code base
or other packages that you need. Which is why there are multiple versions
for you to choose from.

Which version to choose depends on a number of factors, including
the minimum PHP version that is required and whether the package version
is compatible with other packages you need.

However, more important is whether other packages can "require" your package!
If you make the version constraints of required packages to strict
then others will be limited to the version constraints you
have set for the package(s).

    In practice, when your package ``acme/my-package`` requires ``symfony/symfony``
    with version constraint ``~2.3.9`` it is impossible for other packages that
    depend on ``acme/my-package`` to install a newer Symfony version!
    Even though ``acme/my-package`` "is" compatible with newer Symfony versions.

    The ``~2.3.9`` version constraint is short for ``>=2.3.9,<2.4``.

So, as a rule of thumb:

    Never "restrict" maximum minor version for a library package.

Only when the package is to be used as a so called edition-package like the
`Symfony standard-edition`_ you may use specific version constraints.

In fact, it's a good practice to always use specific version constraints for
an edition-package! This reduces the change of unexpected breakage of the project
and ensures an as clean as possible update process.

.. _`Semantic versioning`: http://semver.org/
.. _`Symfony standard-edition`: https://github.com/symfony/symfony-standard/
