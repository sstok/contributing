Testing
=======

* Avoid the `private` keyword in specs.
* Separate setup, exercise, verification, and teardown phases with newlines.
* Don't prefix `it` block descriptions with `should`. Use [Imperative mood]
  instead.

[Imperative mood]: http://en.wikipedia.org/wiki/Imperative_mood

Acceptance Tests
----------------

Use [Behat] for StoryBDD and always write new
scenarios when adding a feature, or update existing stories to
adapt to business requirements changes.

* Avoid scenario titles that add no information, such as "successfully."
* Avoid scenario titles that repeat the feature title.
* Use scenario titles that describe the success and failure paths.
* Use features directory to store feature specs.

...

[Behat]: http://docs.behat.org/

Phpspec
-------

Phpspec is a PHP tool set to drive emergent design by specification.
It is not really a testing tool, but a design instrument, which helps
structuring the objects and how they work together.

* Do not use Phpspec for testing code that is considered
  part of the integration layer.
* RED is good, add or fix the code to make it green.
* RED-GREEN-REFACTOR is the rule.
* When writing examples, **describe** the behavior of the object in present tense.
* Omit the `public` keyword;
* Use underscores (`_`) in the examples;
* Use type hinting to mock and stub classes;
* If your specification is getting too complex, the design is properly wrong or
  you're not using the right tool for the job.
* If you cannot describe something easily, probably you should not be doing it that way.

Unit Tests
----------

* [PhpUnit] should be used for integration, API acceptance and functional tests.
* Use an integration testCase class when performing integration tests.
* Write test names in the same way as in PHPSpec, "it_transforms_a_date";
* Organize the testing suite into multiple logical groups, like: formatters, processor, etc.
* Mark performance and functional tests with `@group performance`
  and `@group functional` respectively.
  
[PhpUnit]: https://phpunit.de/
