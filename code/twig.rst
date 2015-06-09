Twig
====

* Don't disable auto escaping on a global basis!
* When wrapping long lines, keep the method name on the same line of the
  interpolation operator and keep each method argument on its own line.
* Prefer double quotes for attributes.
* Use spaceless to minify output content (unless needed by the output format).

.. code-block:: jinja

    {% short_method_call_that_fits_on_one_line(arguments) %}

    {% link_to(
      some_object_with_a_long_name.title,
      parent_object_child_object_path(some_object_with_a_long_name)
    ) %}
