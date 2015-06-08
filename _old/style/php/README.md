Php
===

Follows the standards defined in the [PSR-1], [PSR-2]
and [PSR-4] documents.

* Don't use PHP short-tags (except for `<?=` in templates).
* Use the strict comparisons `===` and `!==` when possible
* Import all objects that are not in the current or global namespace.
* Imported namespaces must be sorted in alphabetic order.
* Add a blank line before exit-flow statements like `return`, `throw`, `exit`,
  `goto` `break`, `continue` and `yield`, unless the return is alone inside
  a statement-group (like an `if` statement).
* Don't use `return null;` but use `return;` instead.
* Mark public methods that are only to be used.
  as private callback with `@internal`.
* No spaces between the concatenate character `.`.
* Use a short reference like `use Symfony\Component\DependencyInjection\Loader;`
  when importing more then 3 objects from a namespace.
* Use parentheses when instantiating classes regardless of the number of
  arguments the constructor has.
* Exception message strings should be concatenated using `sprintf()`.
* Declare public methods first, then protected ones and finally private ones.
  The exceptions to this rule are the public class constructor and the `setUp` and
  `tearDown` methods of PHPUnit tests, which should always be the first methods
  to increase readability.
* Use namespaces for all classes.

[PSR-1]: http://www.php-fig.org/psr/psr-1/
[PSR-2]: http://www.php-fig.org/psr/psr-2/
[PSR-4]: http://www.php-fig.org/psr/psr-4/

Naming
------

* Use camelCase, not underscores, for variable, function and method
  names, arguments.
* Use underscores for option names and parameter names.
* Use meaningful class and interface names,
  don't use prefixes/suffixes like Interface, Abstract, Trait.
* For type-hinting and casting, use `bool` (instead of `boolean`
  or `Boolean`), `int` (instead of `integer`), `float` (instead of
  `double` or `real`);
* Don't forget to look at the more verbose :doc:`conventions` document for
  more subjective naming considerations.   

Documentation
-------------

* Add PHPDoc blocks for classes, properties, methods, and functions.
* Don't use the `@package` and `@subpackage` annotations.
* Don't use the `@since` or `@deprecated` annotations for a application specific code.
* Don't use the `@author` annotations for proprietary software.
  The actual authorship belongs to the company.
* Only add PHPDoc when this provides an added value, private methods without `@return`
  should not have PHPDoc. Public getters with a clear relation should not have PHPDoc.
* Each comment line should break approximately after the first word that
  crosses the 72nd character (so most lines end up being 72-80 characters).
* PHPDoc Description is limited to 72 chars in the first line, followed
  by an empty line, and a long description when needed.
* All items of the `@param` phpdoc tags must be aligned vertically.
* Add one empty line before the `@return` and `@throws` tags.
* PHPDoc tags are sorted in the following order:
    * `@param`
    * `@throws`
    * `@return`
* Omit the `@return` tag if the class method does not return anything.
* Use `@return null` instead of `@return void` for interfaces.
