Symfony
=======

* Avoid `member` and `collection` routes.
* Name date columns with `_on` suffixes.
* Name datetime columns with `_at` suffixes.

* Define forms as PHP classes.
* Don't register Forms as services when they are not be to extended,
  or embedded in other forms directly or via the collection type.
* Add buttons in the templates, not in the form classes or the controllers.
* Keep application specific themes within the `app/Resources/views` folder.
* Store (compiled) assets in the web/ directory.
* Avoid using Assetic for assets management.
  Use Bower and Gulp/Grunt instead.

Controllers
-----------

* Keep controllers thin, keep as much logic in services.
* Prefer to use ActionControllers (one action per controller)
  rather then one controller per resource.
* Don't inject the ServiceContainer, but use explicit service injection
  and use helper classes for big DI injection (service-provider) with
  with an explicit contract.
* Don't use the `@Template()` annotation to configure the
  template used by the controller.
* A controller must return a Response, unless its not executed.
  Don't rely on services for setting the response during an action.

...

Translations
------------

* Always use keys for translations instead of content strings.
* Translations keys should always describe their purpose and not their location.
  If a form has a field with the label "Username", then a nice key
  would be label.username, not edit_form.label.username.
* Use Yaml for translation files.
* Don't create special translation domains like
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
* Use constant timing comparison for tokens.
* For fine-grained restrictions, define a custom security voter.
* Unless there is two legitimately different authentication systems and users
  (e.g. form login for the main site and a token system for API only),
  use only one firewall entry with the anonymous key enabled.
* For protecting broad URL patterns, use access_control;

Services
--------

* A service name contains groups, separated by dots.
* Use lowercase letters for service and parameter names.
* The DI alias of the bundle is the first group (e.g. `rollerworks_user`).
* If the bundle is a so-called AppBundle, then use `app` instead.
* A group name uses the underscore notation.
* Avoid using a corresponding parameter containing the class name
  `service_name.class`, unless the service is be configurable.

Migrations
----------

[Sample](migration.rb)

* Set an empty string as the default constraint for non-required string and text
  fields. [Example][default example].
* List timestamps first when creating a new table. [Example][timestamps example].

[timestamps example]: migration.rb
[default example]: migration.rb#L6

Routes
------

* Routes must have a method requirement.
* Use Yaml for defining routing files.
* Use annotations only for Controllers that are not to be reused.

...

E-mail
------

* Use the user's name in the `From` header and email in the `Reply-To` when
  delivering email on behalf of the app's users.
* Always include a text-only version when sending HTML.
