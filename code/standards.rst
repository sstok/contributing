Coding Standards
================

When contributing code, you must follow the coding standards. To
make a long story short, here is the golden rule: **Imitate the existing
project code**.

Remember that the main advantage of standards is that every piece of code
looks and feels familiar, it's not about this or that being more readable.

.. toctree::
    :hidden:

    php
    symfony
    twig
    testing

General
-------

* These are not to be blindly followed; strive to understand these and ask
  when in doubt;

* Don't duplicate the functionality of a built-in library;

* Don't swallow exceptions or "fail silently";

* Don't write code that guesses at future functionality;

* `Exceptions should be exceptional`_

* `Keep the code simple`_

* Don't create new anonymous functions in a loop;

Object-Oriented Design
----------------------

* Prefer ``private`` over ``protected``, unless the class is meant to
  be extended;

* A class with a fixed functionality should be marked final;

* Avoid long parameter lists;

* Limit collaborators of an object (entities an object depends on);

* Limit an object's dependencies (entities that depend on an object);

* Prefer composition over inheritance;

* Prefer small methods. Between one and five lines is best;

* Prefer small classes with a single, well-defined responsibility. When a
  class exceeds 100 lines, it may be doing too many things;

* Prefer immutable classes over mutable classes;

* `Tell, don't ask`_

Browsers
--------

* Don't support clients without Javascript;

* Don't support anything lower then IE9;

.. _`Exceptions should be exceptional`: http://www.sitepoint.com/exceptional-exceptions/
.. _`Keep the code simple`: http://www.readability.com/~/ko2aqda2
.. _`Tell, don't ask`: http://robots.thoughtbot.com/post/27572137956/tell-dont-ask
