Twig
====

Here's a short example containing most features described below:

.. code-block:: jinja

    {#
     # This file is part of the PROJECT-name package.
     #
     # (c) Author name <name@example.com>
     #
     # For the full copyright and license information, please view the LICENSE
     # file that was distributed with this source code.
     #}

    {% short_method_call_that_fits_on_one_line(arguments) %}

    {% link_to(
      some_object_with_a_long_name.title,
      parent_object_child_object_path(some_object_with_a_long_name)
    ) %}

* Don't disable auto escaping on a global basis!

* When wrapping long lines, keep the method name on the same line of the
  interpolation operator and keep each method argument on its own line;

* Prefer double quotes for attributes;

* Use spaceless to minify output content (unless needed by the output format);

License
-------

* Code is released under the MIT license, and the license block has to be
  present at the top of every Twig file, before any HTML or Twig tag.
