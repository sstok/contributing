Best Practices
==============

A guide for programming well.

General
-------

* These are not to be blindly followed; strive to understand these and ask
  when in doubt.
* Don't duplicate the functionality of a built-in library.
* Don't swallow exceptions or "fail silently."
* Don't write code that guesses at future functionality.
* [Exceptions should be exceptional].
* [Keep the code simple].
* Don't create new anonymous functions in a loop

[Exceptions should be exceptional]: http://www.sitepoint.com/exceptional-exceptions/
[Keep the code simple]: http://www.readability.com/~/ko2aqda2

Object-Oriented Design
----------------------

* Prefer `private` over `protected`, unless the class is meant to
  be extended.
* A class with a fixed functionality should be marked final.
* Avoid long parameter lists.
* Limit collaborators of an object (entities an object depends on).
* Limit an object's dependencies (entities that depend on an object).
* Prefer composition over inheritance.
* Prefer small methods. Between one and five lines is best.
* Prefer small classes with a single, well-defined responsibility. When a
  class exceeds 100 lines, it may be doing too many things.
* Prefer immutable classes over mutalbe classes.
* [Tell, don't ask].

[Tell, don't ask]: http://robots.thoughtbot.com/post/27572137956/tell-dont-ask

PHP
---

* Use [PHP the right way].
* Avoid global variables.
* Avoid monkey-patching.
* Don't use `$GLOBALS` or `$_REQUEST`.
* Use `$_SERVER[‘ARGS’]` instead of `$ARGS`
* Ensure that all PHP errors (including `E_NOTICE` and `E_DEPRECATED`)
  are shown during development and testing.
* Disable PHP short-tags.
* Disallow persistent database connections.
* Configure the proper timezone (in which the server is located).
* Use [Composer] for managing package dependencies.
* Avoid a hard coupling to the environment settings.
    * Do not hard code API tokens, security keys or passwords
    * Do not rely upon the Application environment settings (except for debug),
      use changeable configurations that differ per application environment.
      
[PHP the right way]: http://www.phptherightway.com/
[Composer]: https://getcomposer.org/
[Travis CI]: http://travis-ci.org
      
Composer
--------

* Specify the PHP version to be used on the project in the composer.json
* Specify the PHP extensions to be used on the project in the composer.json
* Specify the PHP version and extensions as minimum, don't specify a maximum
  PHP version.
* Avoid specifying version bounds without a limit like `>=2.0`
* Include a link to the contributes list.

TODO Version constraints for packages and applications.
   
Symfony
-------

* Know your way around in the land of PHP, web application and Symfony security. Don’t
  trust “the framework” blindly. And when you have set up your security preventions: know
  if and why they work.
* Prefer to use at minimum a supported long term support (LTS) version.
* Prefer to use Twig as template engine.
* Avoid binding a Form directly to a Domain Model.
* Avoid having a hard dependency on the ServiceContainer.
* Change the default session-name.
* Prefer httponly over an unprotected cookies to [prevent tampering].
* Invalidate session after logout.

[prevent tampering]: http://blog.bigbinary.com/2013/03/19/cookies-on-rails.html

Doctrine ORM
------------

* Keep migrations under version control.
* Don't change a migration after it has been merged into master if the desired
  change can be solved with another migration.
* Use caching for better performance.
* Don't use annotations for configuring mapping-data.

Testing
-------

* Unit tests must be small, easy to understand and fast
  (less then a minute per test).
* Use the best testing method for the current situation.  
* Avoid [over-testing].
* Production tests should not take longer then one hour max.
* Never use production data when mocked-up or faked data is available.
* Test at least once in an environment similar to the production system,
  also known as staging.
* Only perform the API acceptance tests when the related code has changed.
* Do not rely on the order of execution when using stubs/mocks.
  Relying on the order of execution makes tests more fragile and harder to debug,
  use the [Prophecy] library for mocking.
* Disable real HTTP requests to external services.
* Don't test private methods.
* Use [stubs and spies] \(not mocks\) in isolated tests.
* Use a single level of abstraction within scenarios.
* Use integration tests to execute the entire app.
* Use non-[SUT] methods in expectations when possible.

[over-testing]: http://verraes.net/2014/12/how-much-testing-is-too-much/
[stubs and spies]: http://php-and-symfony.matthiasnoback.nl/2014/07/test-doubles/
[SUT]: http://xunitpatterns.com/SUT.html
[Prophecy]: https://github.com/phpspec/prophecy

Postgres
--------

* Avoid multi column indexes in Postgres. It [combines multiple indexes]
  efficiently. Optimize later with a [compound index] if needed.
* Consider a [partial index] for queries on booleans.
* Constrain most columns as [`NOT NULL`].
* [Index foreign keys].

[`NOT NULL`]: http://www.postgresql.org/docs/9.1/static/ddl-constraints.html#AEN2444
[combines multiple indexes]: http://www.postgresql.org/docs/9.1/static/indexes-bitmap-scans.html
[compound index]: http://www.postgresql.org/docs/9.2/static/indexes-bitmap-scans.html
[partial index]: http://www.postgresql.org/docs/9.1/static/indexes-partial.html
[Index foreign keys]: https://tomafro.net/2009/08/using-indexes-in-rails-index-your-associations

Background Jobs
---------------

* Store IDs, not `Model` objects for cleaner serialization, then re-find
  the `Model` object in the `perform` method.

E-mail
------

* Use a tool like [MailView] to look at each created or updated mailer view
  before merging.
* Test sure the e-mail is renderable in most commonly used mail clients.

[MailView]: https://github.com/37signals/mail_view

JavaScript
----------

* Use CoffeeScript.

HTML
----

* Don't use a reset button for forms.
* Prefer cancel links to cancel buttons.
* Use `<button>` tags over `<a>` tags for actions.

CSS
---

* Use Sass.

Sass
----

* Prefer `overflow: auto` to `overflow: scroll`, because `scroll` will always
  display scrollbars outside of OS X, even when content fits in the container.
* Use `image-url` and `font-url`, not `url`, so the asset pipeline will re-write
  the correct paths to assets.
* Prefer mixins to `@extend`.

Browsers
--------

* Don't support clients without Javascript.
* Don't support IE6 or IE7.

Shell
-----

* Don't parse the output of `ls`. See [here][parsingls] for details and
  alternatives.
* Don't use `cat` to provide a file on `stdin` to a process that accepts
  file arguments itself.
* Don't use `echo` with options, escapes, or variables (use `printf` for those
  cases).
* Don't use a `/bin/sh` [shebang][] unless you plan to test and run your
  script on at least: Actual Sh, Dash in POSIX-compatible mode (as it
  will be run on Debian), and Bash in POSIX-compatible mode (as it will
  be run on OSX).
* Don't use any non-POSIX [features][bashisms] when using a `/bin/sh`
  [shebang][].
* If calling `cd`, have code to handle a failure to change directories.
* If calling `rm` with a variable, ensure the variable is not empty.
* Prefer "$@" over "$\*" unless you know exactly what you're doing.
* Prefer `awk '/re/ { ... }'` to `grep re | awk '{ ... }'`.
* Prefer `find -exec {} +` to `find -print0 | xargs -0`.
* Prefer `for` loops over `while read` loops.
* Prefer `grep -c` to `grep | wc -l`.
* Prefer `mktemp` over using `$$` to "uniquely" name a temporary file.
* Prefer `sed '/re/!d; s//.../'` to `grep re | sed 's/re/.../'`.
* Prefer `sed 'cmd; cmd'` to `sed -e 'cmd' -e 'cmd'`.
* Prefer checking exit statuses over output in `if` statements (`if grep
  -q ...; `, not `if [ -n "$(grep ...)" ];`).
* Prefer reading environment variables over process output (`$TTY` not
  `$(tty)`, `$PWD` not `$(pwd)`, etc).
* Use `$( ... )`, not backticks for capturing command output.
* Use `$(( ... ))`, not `expr` for executing arithmetic expressions.
* Use `1` and `0`, not `true` and `false` to represent boolean
  variables.
* Use `find -print0 | xargs -0`, not `find | xargs`.
* Use quotes around every `"$variable"` and `"$( ... )"` expression
  unless you want them to be word-split and/or interpreted as globs.
* Use the `local` keyword with function-scoped variables.
* Identify common problems with [shellcheck][].

[shebang]: http://en.wikipedia.org/wiki/Shebang_(Unix)
[parsingls]: http://mywiki.wooledge.org/ParsingLs
[bashisms]: http://mywiki.wooledge.org/Bashism
[shellcheck]: http://www.shellcheck.net/

Bash
----

In addition to Shell best practices,

* Prefer `${var,,}` and `${var^^}` over `tr` for changing case.
* Prefer `${var//from/to}` over `sed` for simple string replacements.
* Prefer `[[` over `test` or `[`.
* Prefer process substitution over a pipe in `while read` loops.
* Use `((` or `let`, not `$((` when you don't need the result

Haskell
-------

* Avoid partial functions (`head`, `read`, etc).
* Compile code with `-Wall -Werror`.

Ember
-----

* Avoid using `$` without scoping to `this.$` in views and components.
* Prefer to make model lookup calls in routes instead of controllers (`find`,
  `findAll`, etc.).
* Prefer adding properties to controllers instead of models.
* Don't use jQuery outside of views and components.
* Prefer to use predefined `Ember.computed.*` functions when possible.
* Use `href="#"` for links that have an action.
* Prefer dependency injection through Ember initializers over globals on window
  or namespaces.

Angular
-------

* Prefer `factory` to `service`. If you desire a singleton, wrap the singleton
  class in a factory function and return a new instance of that class from the
  factory.
* Prefer the `translate` directive to the `translate` filter for [performance
  reasons][angular-translate].
* Don't use the `jQuery` or `$` global. Access jQuery via `angular.element`.

[angular-translate]: https://github.com/angular-translate/angular-translate/wiki/Getting-Started#using-translate-directive
