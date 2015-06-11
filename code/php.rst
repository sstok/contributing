Php
===

Styling
-------

Follows the standards defined in the `PSR-1`_, `PSR-2`_
and `PSR-4`_ documents.

Since a picture - or some code - is worth a thousand words, here's a short
example containing most features described below:

.. code-block:: html+php

    <?php

    /*
     * This file is part of the PROJECT-name package.
     *
     * (c) Author name <name@example.com>
     *
     * For the full copyright and license information, please view the LICENSE
     * file that was distributed with this source code.
     */

    namespace Acme;

    /**
     * Coding standards demonstration.
     */
    class FooBar
    {
        const SOME_CONST = 42;

        private $fooBar;

        /**
         * @param string $dummy Some argument description
         */
        public function __construct($dummy)
        {
            $this->fooBar = $this->transformText($dummy);
        }

        /**
         * @param string $dummy Some argument description
         * @param array  $options
         *
         * @return string|null Transformed input
         *
         * @throws \RuntimeException
         */
        private function transformText($dummy, array $options = array())
        {
            $mergedOptions = array_merge(
                array(
                    'some_default' => 'values',
                    'another_default' => 'more values',
                ),
                $options
            );

            if (true === $dummy) {
                return;
            }

            if ('string' === $dummy) {
                if ('values' === $mergedOptions['some_default']) {
                    return substr($dummy, 0, 5);
                }

                return ucwords($dummy);
            }

            throw new \RuntimeException(sprintf('Unrecognized dummy option "%s"', $dummy));
        }
    }

* Add a single space after each comma delimiter;

* Add a single space around operators (``==``, ``&&``, ...);

* Add a comma after each array item in a multi-line array, even after the
  last one;

* Add a blank line before ``return`` statements, unless the return is alone
  inside a statement-group (like an ``if`` statement);

* Use braces to indicate control structure body regardless of the number of
  statements it contains;

* Define one class per file - this does not apply to private helper classes
  that are not intended to be instantiated from the outside and thus are not
  concerned by the `PSR-4`_ standard;

* Declare class properties before methods;

* Declare public methods first, then protected ones and finally private ones;
  The exceptions to this rule are the class constructor and the ``setUp`` and
  ``tearDown`` methods of PHPUnit tests, which should always be the first methods
  to increase readability;

* Use parentheses when instantiating classes regardless of the number of
  arguments the constructor has;

* Exception message strings should be concatenated using :phpfunction:`sprintf`;

* Use the strict comparisons ``===`` and ``!==`` when possible

* Import all objects that are not in the current or global namespace;

* Imported namespaces must be sorted in alphabetic order;

* Add a blank line before exit-flow statements like ``return``, ``throw``, ``exit``,
  ``goto`` ``break``, ``continue`` and ``yield``, unless the return is alone inside
  a statement-group (like an ``if`` statement);

* Don't use ``return null;`` but use ``return;`` instead;

* Implemented interface methods with no functionality must be commented with ``// noop``
  (*noop is short for no operation*);

* Mark public methods that are only to be used;
  as private callback with ``@internal``;

* No spaces between the concatenate character ``.``;

* Use a short reference like ``use Symfony\Component\DependencyInjection\Loader;``
  when importing more then 3 objects from a namespace;

* Use parentheses when instantiating classes regardless of the number of
  arguments the constructor has;

* Exception message strings should be concatenated using ``sprintf()``;

* Declare public methods first, then protected ones and finally private ones;
  The exceptions to this rule are the public class constructor and the ``setUp`` and
  ``tearDown`` methods of PHPUnit tests, which should always be the first methods
  to increase readability;

* Use namespaces for all classes;

Naming
~~~~~~

* Use camelCase, not underscores, for variable, function and method
  names, arguments;

* Use underscores for option names and parameter names;

* Use meaningful class and interface names,
  don't use prefixes/suffixes like Interface, Abstract, Trait;

* For type-hinting and casting, use ``bool`` (instead of ``boolean``
  or ``Boolean``), ``int`` (instead of ``integer``), ``float`` (instead of
  ``double`` or ``real``);

* Don't forget to look at the more verbose :doc:`conventions` document for
  more subjective naming considerations;

Documentation
~~~~~~~~~~~~~

Follows the standards defined in the `PSR-5`_ document.

* Add PHPDoc blocks for classes, properties, methods, and functions;

* Don't use the ``@package`` and ``@subpackage`` annotations;

* Don't use the ``@since`` or ``@deprecated`` annotations for a application specific code;

* Don't use the ``@author`` annotations for proprietary software;
  The actual authorship belongs to the company;

* Only add PHPDoc when this provides an added value, private methods without ``@return``
  should not have PHPDoc. Public getters with a clear relation should not have PHPDoc;

* Each comment line should break approximately after the first word that
  crosses the 72nd character (so most lines end up being 72-80 characters);

* PHPDoc Description is limited to 72 chars in the first line, followed
  by an empty line, and a long description when needed;

* All items of the ``@param`` phpdoc tags must be aligned vertically;

* Add one empty line before the ``@return`` and ``@throws`` tags;

* PHPDoc tags are sorted in the following order:
    * ``@param``
    * ``@throws``
    * ``@return``

* Omit the ``@return`` tag if the class method does not return anything;

License
-------

* Code is released under the MIT license, and the license block has to be
  present at the top of every PHP file, before the namespace.

Best Practices
--------------

See also :doc:`best-practices`

* Use `PHP the right way`_;

* Avoid global variables;

* Avoid monkey-patching;

* Don't use ``$GLOBALS`` or ``$_REQUEST``;

* Use ``$_SERVER[‘ARGS’]`` instead of ``$ARGS``

* Ensure that all PHP errors (including ``E_NOTICE`` and ``E_DEPRECATED``)
  are shown during development and testing;

* Disable PHP short-tags;

* Disallow persistent database connections;

* Configure the proper timezone (in which the server is located);

* Use `Composer`_ for managing package dependencies;
    * Regularly update your local Composer installation;
    * Don't add PHPUnit or tools (like php-cs-fixer) as a dev-requirement
      but use the Phar archive instead;
    * Always use a secure connection for downloading Composer, package information
      and the actual package source. Never downgrade to plain HTTP!!,
      If TLS is not available then fix this, you can't trust a package that is
      not provided over a secure connection;
    * Use ``composer require package-name`` or ``composer --dev require package-name`` (for dev requirements)
      to get the best available version;

* Avoid a hard coupling to the environment settings;
    * Do not hard code API tokens, security keys or passwords;
    * Do not rely upon the Application environment settings (except for debug),
      use changeable configurations that differ per application environment;

.. _`PHP the right way`: http://www.phptherightway.com/
.. _`PSR-1`: http://www.php-fig.org/psr/psr-1/
.. _`PSR-2`: http://www.php-fig.org/psr/psr-2/
.. _`PSR-4`: http://www.php-fig.org/psr/psr-4/
.. _`PSR-5`: http://www.php-fig.org/psr/psr-5/
.. _`Composer`: https://getcomposer.org/
