Style
=====

Delivering valuable features and working software are our ultimate goals.
 
This style guide should be used in service of those goals, and not as an
end in itself. Your time is valuable.

In addition to the general guidelines below, we also have the following more
detailed, language/framework-specific style guides:

* [Backbone](backbone)
* [CoffeeScript](coffeescript)
* [Ember.js](ember)
* [Twig](twig)
* [Git](git)
* [Haskell](haskell)
* [HTML](html)
* [Python](python)
* [Symfony](symfony)
* [Sass](sass)
* [Shell](shell)
* [Testing](testing)

Formatting
----------

* Avoid inline comments.
* Avoid keeping the Copyright year range in the file header,
  Use the LICENSE and/or README instead.
* Break long lines after 80 characters.
* Delete trailing whitespace.
* Don't include spaces after `(`, `[` or before `]`, `)`.
* Don't misspell.
* Don't vertically align tokens on consecutive lines.
* Use strict comparisons `===` and `!==` when possible;
* If you break up an argument list, keep the arguments on their own lines and
  closing parenthesis on its own line.
* If you break up a hash, keep the elements on their own lines and closing curly
  brace on its own line.
* Indent continued lines two spaces.
* Indent private methods equal to public methods.
* Use 4 space indentation (no tabs).
* Use an empty line between methods.
* Use empty lines around multi-line blocks.
* Use spaces around operators, except for unary operators, such as `!`.
* Use spaces after commas, after colons and semicolons, around `{` and before `}`.
* Use [Unix-style line endings] (`\n`).
* Use [uppercase for SQL key words and lowercase for SQL identifiers].
* Use braces to indicate control structure body regardless of the number of
  statements it contains;
* Use so-called Yoda conditions for (not) equals comparisons (``value === $var``)
* Declare class properties before methods.

[uppercase for SQL key words and lowercase for SQL identifiers]: http://www.postgresql.org/docs/9.2/static/sql-syntax-lexical.html#SQL-SYNTAX-IDENTIFIERS
[Unix-style line endings]: http://unix.stackexchange.com/questions/23903/should-i-end-my-text-script-files-with-a-newline

Naming
------

* Avoid abbreviations.
* Avoid object types in names (`user_array`, `email_method` `CalculatorClass`, `ReportModule`).
* Avoid names that have a broad meaning. A ``User`` object with a ``name`` property is considered
  a code smell. The ``name`` in this content can mean multiple things:
  the login name, the real name or display name. Better is `displayName`.
* Don't use “Hungarian notation” - https://en.wikipedia.org/wiki/Hungarian_notation
* Prefer naming classes after domain concepts rather than patterns they
  implement (e.g. `Guest` vs `NullUser`, `CachedRequest` vs `RequestDecorator`).
* Use alphanumeric characters and underscores for file names.
* Use plurals and singular correctly, variable `users` holds a collections
  of Users, while `user` is a single users.
* Name variables created by a factory after the factory (`userFactory`
  creates `user`).
* Name variables, methods, and classes to reveal intent.
* Treat acronyms as words in names (`XmlHttpRequest` not `XMLHTTPRequest`),
  even if the acronym is the entire name (`class Html` not `class HTML`).
* Suffix variables holding a factory with `Factory` (`userFactory`).

Organization
------------

* Order methods so that caller methods are earlier in the file than the methods
  they call.
* Order methods so that methods are as close as possible to other methods they
  call.
  
License
-------

* Each project is released under its own license, and the license block has to be
  present at the top of every file directly after the opening tag `<?php`, `<?xml ...>`.
* Mention the license type clearly.
* Include "Redistribution and reproduction in source and binary forms,
  with or without modification is prohibited." for proprietary private software.
