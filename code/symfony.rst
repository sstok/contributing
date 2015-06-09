Symfony
=======

    Symfony already has a set `Best Practices`_, but as these Best Practices
    are more focused on beginners we may not follow them everywhere.
    In the end its not whether they or we are better, but what works for
    the project itself.
    
General
-------

* Define forms as PHP classes.
* Don't register Forms as services when they are not be to extended,
  or embedded in other forms directly or via the collection type.
* Add buttons in the templates, not in the form classes or the controllers.
* Keep application specific themes within the ``app/Resources/views`` folder.
* Store (compiled) assets in the web/ directory.
* Avoid using Assetic for assets management.
  Use Bower and Gulp instead.
  
Controllers
-----------

* Keep controllers thin, keep as much logic in services.
* Don't inject the ServiceContainer, but use explicit service injection
  and use helper classes for big DI injection (service-provider) with
  with an explicit contract.
* Don't use the ``@Template()`` annotation to configure the
  template used by the controller.

Translations
------------

* Always use keys for translations instead of content strings.
* Translations keys should always describe their purpose and not their location.
  If a form has a field with the label "Username", then a nice key
  would be label.username, not edit_form.label.username.
* Use Yaml for translation files.
* Don't create special translation domains for bundles/components like
  "AcmeUser" or "forms" but use the "messages" domain instead.
* Keep translations per logical domain:
    * validations: holds validation violation messages.
    * navigation: translations related to navigation, including
      the "menu" and "breadcrumbs".
    * search: field alias en labels for RollerworksSearch.
    * messages: translations with no specific domain.
  
Security
--------

* Use bcrypt for password encoding.
* Use constant timing comparison for (security) tokens.
* For fine-grained restrictions, define a custom security voter.
* Unless there are two legitimately different authentication and user systems
  (e.g. a form login for the main site and a token system for a REST API),
  use only one firewall entry with the anonymous key enabled.
* For protecting broad URL patterns, use access_control.
* Always perform the authentication using SSL (when available).

Services
--------

* A service name contains groups, separated by dots.
* Use lowercase letters for service and parameter names.
* The DI alias of the bundle is the first group (e.g. ``rollerworks_search``).
* If the bundle is an AppBundle, then use ``app`` instead.
* A group name uses the underscore notation.
* Avoid using a corresponding parameter containing the class name
  ``service_name.class``, unless the service-class must be changeable.
  
.. note::

    At the moment there is no preferred file format (Yaml or XML)
    for defining service definitions.
    
    XML is most preferred for the moment, as it supports XSD validation
    and autosuggest in most IDE's but Yaml can be typed faster.
    *Also, some PHP installations have a broken XML parser.*
    
    Which ever format is chosen, it is applied consistently.
    Don't mix service definition formats within a single project.
    
Routes
------

* Routes must have a method requirement.
* Use Yaml for defining routing files.
* Use annotations only for Controllers that are not to be reused.

E-mail
------

* Use the user's name in the ``From`` header and email in the ``Reply-To`` when
  delivering email on behalf of the app's users.
* Always include a text-only version when sending HTML.

Doctrine ORM
------------

* Name date columns with ``_on`` suffixes.
* Name datetime columns with ``_at`` suffixes.
* Don't mark Entity classes as final (this breaks lazy loading).
* Don't hard code the EntityManager name (keep this configurable). 

.. _`Best Practices`: http://symfony.com/doc/current/best_practices/index.html
