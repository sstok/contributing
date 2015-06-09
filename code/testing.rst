Testing
=======

* Avoid the ``private`` keyword in specs.
* Don't prefix ``it`` block descriptions with ``should``. Use `Imperative mood`_
  instead.

Acceptance Tests
----------------

Use `Behat`_ for StoryBDD and always write new scenarios when adding a
feature, or update existing stories to adapt to business requirements
changes.

*Remember you are writing a "business requirement" that describes "what"
the requirement is not "how" the requirement is fulfilled.*

* Avoid scenario titles that add no information, such as "successfully."
* Avoid scenario titles that repeat the feature title.
* Use scenario titles that describe the success and failure paths.
* Avoid describing technical actions ( `Introducing Modelling by Example`_ );
    * "When I click"
    * "And I go to the "/basket" page"
* Use the features directory to store feature specs.

Phpspec
-------

Phpspec is a PHP tool set to drive emergent design by specification.
It is not really a testing tool, but a design instrument, which helps
structuring the objects and how they work together.

* Don't use Phpspec for testing code that is considered
  part of the integration layer.
* RED is good, add or fix the code to make it green.
* RED-GREEN-REFACTOR is the rule.
* When writing examples, **describe** the behavior of the object in present tense.
* Omit the ``public`` keyword;
* Use underscores (``_``) in the examples;
* Use type hinting to mock and stub classes;
* If your specification is getting too complex, the design is properly wrong or
  you're not using the right tool for the job.
* If you cannot describe something easily, probably you should not be doing it that way.

Unit Tests
----------

* `PhpUnit`_ should be used for integration, API acceptance and functional tests.
* Use an integration testCase class when performing integration tests.
* Organize the testing suite into multiple logical groups, like: formatters, processor, etc.
* Mark performance and functional tests with ``@group performance``
  and ``@group functional`` respectively.
* If its not part of the end-expectation, don't mock it.
    * Knowing something should (not) be executed/called is a part of the end-expectation.
        * This includes caching and callbacks/subscribers.
    * In "detail" mocking something to get a result breaks this principle.
    
Don't mock type you don't own!
------------------------------

*This is not a hard line, but crossing this line may have repercussions! (it most likely will)*

1. Imagine code that mocks a third party library. After a particular upgrade of a third library,
   the logic might change a bit, but the test suite will execute just fine, because it's mocked.
   So later on, thinking everything is good to go, the build-wall is green after all, the software is
   deployed and... *Boom*
2. It may be a sign that the current design is not decoupled enough from this third party library.
3. Also another issue is that the third party lib might be complex and require a lot of mocks to even work properly.
   That leads to overly specified tests and complex fixtures, which in itself compromises the *compact and
   readable* goal. Or to tests which do not cover the code enough, because of the complexity to mock the
   external system.

Instead, the most common way is to create wrappers around the external lib/system, though one should be aware
of the risk of *abstraction leakage*, where too much low level API, concepts or exceptions, goes beyond the
boundary of the wrapper. In order to verify integration with the third party library, write integration tests,
and make them as *compact and readable* as possible as well.

Other people have already written on the matter and experienced pain when mocking a type they didn't own:

* http://davesquared.net/2011/04/dont-mock-types-you-dont-own.html
* http://www.markhneedham.com/blog/2009/12/13/tdd-only-mock-types-you-own
* http://blog.8thlight.com/eric-smith/2011/10/27/thats-not-yours.html
* http://stackoverflow.com/questions/1906344/should-you-only-mock-types-you-own

Don't mock everything, it's an anti-pattern
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If everything is mocked, are we really testing the production code?
Don't hesitate to **not** mock!

Don't mock business logic
~~~~~~~~~~~~~~~~~~~~~~~~~

    Business logic or domain logic is the part of the program that encodes the real-world
    business rules that determine how data can be created, displayed, stored, and changed.

In practice Business logic includes (but is not limited) to ValueObjects, Aggregate(Root)
Domain messages, event objects and data Models.
 
In most cases it should not be possible in the first place to mock these objects
as they are marked final.

Why shouldn't you mock this logic? Because its not an interface! Business logic
describes some very specific rules about the application, logic that must (*not should*)
be followed strictly!

If it's too difficult to create new fixtures, it is a sign the code may need some serious refactoring.
An alternative is to create builders for your value objects. One can also create meaningful factory methods
in the test.

Originally based on: https://github.com/mockito/mockito/wiki/How-to-write-good-tests
  
Test naming rules
-----------------

A test/spec ensures something is possible with the subject, it "can do" or "does something".
It does not describe "what" a subject does or is "described" to do.

Name your tests like you name your methods: short, descriptive and explicit.

.. tip::

    A sentences with "and" or "then" maybe an indication the test is doing to much.

* Avoid using articles: "the", "a" "an".
* Avoid using: "then", "it", "its".
* Prefer using "when" instead of "if".

Avoid using "is" when there is already a state indication:

**Bad:**

* is in debug
* is in collection

**Good:**

* in debug
* is debug
* in collection
* is connected
 
Unit tests
~~~~~~~~~~

In unit tests the test class itself always corresponds to the class
that is being tested.
    
.. note::

    Because there is no hard contract (test does not describe what the subject does),
    it's acceptable to use "should" like "ShouldReadColorsWhenFalseInConfigurationFile".

Some examples on how to compose a unit test name:

* "[property] can be [actioned]"
* "should [throw, render, connect, etc.] when [condition] [in, is] [expected condition result]"
* "[subject property/information] Is [perform expected. like: ReadCorrectly, WrittenCorrect]"
* "Can be [actioned] [to, with, from, in, etc] [object]"

Final examples:

* ConfigurationTest:
    * Listener Configuration is read correctly
* MoneyTest:
    * Amount can be retrieved
    * Currency can be retrieved
    * Another money object with same currency can be added
    * Another money object with same currency can be subtracted
    * Can be negated
    * Can be multiplied by a factor
    * Can be allocated to number of targets
    * Can be allocated by ratios
    * Can be compared to another money object with same currency
* DateTimeTypeTest:
    * Can be created
    * ViewTimezone can be transformed to ModelTimezone
    * Invalid Input should fail transformation
    * Time pattern can be configured (alternatively: Time pattern is configurable)
    * Pattern can be configured
    
Specs
~~~~~

Some examples on how to compose a spec "example" title:

* it [actions] [property]
* it will throw when [condition]
* its a [type name]

Final examples:

* UserIdSpec
    * its an identity
    * it is convertible to a string
    * it is comparable to another object

.. _`Imperative mood`: http://en.wikipedia.org/wiki/Imperative_mood
.. _`Behat`: http://docs.behat.org/
.. _`Introducing Modelling by Example`: http://everzet.com/post/99045129766/introducing-modelling-by-example
.. _`PhpUnit`: https://phpunit.de/
