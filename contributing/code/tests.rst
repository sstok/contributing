.. _running-tests:

.. This is very specific for Symfony, we may strip out this section
.. completely.

Running Tests
=============

Before submitting a :doc:`patch <patches>` for inclusion, you need to run the
test suite to check that you have not broken anything.




PHPUnit
-------

To run the test suite, `install PHPUnit`_ 4.5 (or later) first.

Dependencies (optional)
-----------------------

To run the entire test suite, including tests that depend on external
dependencies, php needs to be able to autoload them. By default, they are
autoloaded from ``vendor/`` under the main root directory (see
``autoload.php.dist``).

To install them all, use `Composer`_:

Step 1: Get `Composer`_

.. code-block:: bash

    $ curl -s http://getcomposer.org/installer | php

Make sure you download ``composer.phar`` in the same folder where
the ``composer.json`` file is located.

Step 2: Install vendors

.. code-block:: bash

    $ php composer.phar install

.. note::

    Note that the script takes some time to finish.

.. note::

    If you don't have ``curl`` installed, you can also just download the ``installer``
    file manually at http://getcomposer.org/installer. Place this file into your
    project and then run:

    .. code-block:: bash

        $ php installer
        $ php composer.phar install

After installation, you can update the vendors to their latest version with
the follow command:

.. code-block:: bash

    $ php composer.phar update

Running
-------

First, update the vendors (see above).

Then, run the test suite from the root directory with the following
command:

.. code-block:: bash

    $ phpunit

The output should display ``OK``. If not, you need to figure out what's going on
and if the tests are broken because of your modifications.

.. tip::

    If you want to test a single component type its path after the ``phpunit``
    command, e.g.:

    .. code-block:: bash

        $ phpunit src/Finder/

.. tip::

    Run the test suite before applying your modifications to check that they
    run fine on your configuration.

PHPSpec
-------

Some projects may instead or additionally also require PhpSpec for testing.
Whenever


.. _install PHPUnit: http://www.phpunit.de/manual/current/en/installation.html
.. _`Composer`: http://getcomposer.org/
