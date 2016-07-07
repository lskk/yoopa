Kustomisasi Template
====================

Referensi cara kustomisasi template adalah di `Twig Template naming conventions - Drupal <https://www.drupal.org/node/2354645>`_.

Nodes
-----

Pattern: ``node--[type|nodeid]--[viewmode].html.twig``
Base template: ``node.html.twig`` (base location: ``core/modules/node/templates/node.html.twig``)

Theme hook suggestions are made based on these factors, listed from the most specific template to the least. Drupal will use the most specific template it finds:

1. ``node--nodeid--viewmode.html.twig``
2. ``node--nodeid.html.twig``
3. ``node--type--viewmode.html.twig``
4. ``node--type.html.twig``
5. ``node--viewmode.html.twig``
6. ``node.html.twig``

Note that underscores in a content type's machine name are replaced by hyphens.

See the `node.html.twig API documentation <https://api.drupal.org/api/drupal/core!modules!node!templates!node.html.twig/8>`_.

node.html.twig
~~~~~~~~~~~~~~

1. 8.2.x core/themes/bartik/templates/node.html.twig
2. 8.2.x core/themes/classy/templates/content/node.html.twig
3. 8.2.x core/modules/statistics/tests/themes/statistics_test_attached/node.html.twig
4. 8.2.x core/modules/system/tests/themes/test_theme/templates/node.html.twig
5. 8.2.x core/modules/node/templates/node.html.twig
6. 8.2.x core/themes/stable/templates/content/node.html.twig

Default theme implementation to display a node.

Available variables:

- node: The node entity with limited access to object properties and methods. Only method names starting with "get", "has", or "is" and a few common methods such as "id", "label", and "bundle" are available. For example:
    - node.getCreatedTime() will return the node creation timestamp.
    - node.hasField('field_example') returns TRUE if the node bundle includes field_example. (This does not indicate the presence of a value in this field.)
    - node.isPublished() will return whether the node is published or not.
  Calling other methods, such as node.delete(), will result in an exception. See \Drupal\node\Entity\Node for a full list of public properties and methods for the node object.

- label: The title of the node.
- content: All node items. Use {{ content }} to print them all, or print a subset such as {{ content.field_example }}. Use {{ content|without('field_example') }} to temporarily suppress the printing of a given child element.
- author_picture: The node author user entity, rendered using the "compact" view mode.
- metadata: Metadata for this node.
- date: Themed creation date field.
- author_name: Themed author name field.
- url: Direct URL of the current node.
- display_submitted: Whether submission information should be displayed.
- attributes: HTML attributes for the containing element. The attributes.class element may contain one or more of the following classes:
    - node: The current template type (also known as a "theming hook").
    - node--type-[type]: The current node type. For example, if the node is an "Article" it would result in "node--type-article". Note that the machine name will often be in a short form of the human readable label.
    - node--view-mode-[view_mode]: The View Mode of the node; for example, a teaser would result in: "node--view-mode-teaser", and full: "node--view-mode-full".

    The following are controlled through the node publishing options.

    - node--promoted: Appears on nodes promoted to the front page.
    - node--sticky: Appears on nodes ordered above other non-sticky nodes in teaser listings.
    - node--unpublished: Appears on unpublished nodes visible only to site admins.

- title_attributes: Same as attributes, except applied to the main title tag that appears in the template.
- content_attributes: Same as attributes, except applied to the main content tag that appears in the template.
- author_attributes: Same as attributes, except applied to the author of the node tag that appears in the template.
- title_prefix: Additional output populated by modules, intended to be displayed in front of the main title tag that appears in the template.
- title_suffix: Additional output populated by modules, intended to be displayed after the main title tag that appears in the template.
- view_mode: View mode; for example, "teaser" or "full".
- teaser: Flag for the teaser state. Will be true if view_mode is 'teaser'.
- page: Flag for the full page state. Will be true if view_mode is 'full'.
- readmore: Flag for more state. Will be true if the teaser content of the node cannot hold the main body content.
- logged_in: Flag for authenticated user status. Will be true when the current user is a logged-in member.
- is_admin: Flag for admin user status. Will be true when the current user is an administrator.

@todo Remove the id attribute (or make it a class), because if that gets rendered twice on a page this is invalid CSS for example: two lists in different view modes.

File
~~~~

core/modules/node/templates/node.html.twig

::

    {#
    /**
    * @file
    * Default theme implementation to display a node.
    *
    * Available variables:
    * - node: The node entity with limited access to object properties and methods.
    *   Only method names starting with "get", "has", or "is" and a few common
    *   methods such as "id", "label", and "bundle" are available. For example:
    *   - node.getCreatedTime() will return the node creation timestamp.
    *   - node.hasField('field_example') returns TRUE if the node bundle includes
    *     field_example. (This does not indicate the presence of a value in this
    *     field.)
    *   - node.isPublished() will return whether the node is published or not.
    *   Calling other methods, such as node.delete(), will result in an exception.
    *   See \Drupal\node\Entity\Node for a full list of public properties and
    *   methods for the node object.
    * - label: The title of the node.
    * - content: All node items. Use {{ content }} to print them all,
    *   or print a subset such as {{ content.field_example }}. Use
    *   {{ content|without('field_example') }} to temporarily suppress the printing
    *   of a given child element.
    * - author_picture: The node author user entity, rendered using the "compact"
    *   view mode.
    * - metadata: Metadata for this node.
    * - date: Themed creation date field.
    * - author_name: Themed author name field.
    * - url: Direct URL of the current node.
    * - display_submitted: Whether submission information should be displayed.
    * - attributes: HTML attributes for the containing element.
    *   The attributes.class element may contain one or more of the following
    *   classes:
    *   - node: The current template type (also known as a "theming hook").
    *   - node--type-[type]: The current node type. For example, if the node is an
    *     "Article" it would result in "node--type-article". Note that the machine
    *     name will often be in a short form of the human readable label.
    *   - node--view-mode-[view_mode]: The View Mode of the node; for example, a
    *     teaser would result in: "node--view-mode-teaser", and
    *     full: "node--view-mode-full".
    *   The following are controlled through the node publishing options.
    *   - node--promoted: Appears on nodes promoted to the front page.
    *   - node--sticky: Appears on nodes ordered above other non-sticky nodes in
    *     teaser listings.
    *   - node--unpublished: Appears on unpublished nodes visible only to site
    *     admins.
    * - title_attributes: Same as attributes, except applied to the main title
    *   tag that appears in the template.
    * - content_attributes: Same as attributes, except applied to the main
    *   content tag that appears in the template.
    * - author_attributes: Same as attributes, except applied to the author of
    *   the node tag that appears in the template.
    * - title_prefix: Additional output populated by modules, intended to be
    *   displayed in front of the main title tag that appears in the template.
    * - title_suffix: Additional output populated by modules, intended to be
    *   displayed after the main title tag that appears in the template.
    * - view_mode: View mode; for example, "teaser" or "full".
    * - teaser: Flag for the teaser state. Will be true if view_mode is 'teaser'.
    * - page: Flag for the full page state. Will be true if view_mode is 'full'.
    * - readmore: Flag for more state. Will be true if the teaser content of the
    *   node cannot hold the main body content.
    * - logged_in: Flag for authenticated user status. Will be true when the
    *   current user is a logged-in member.
    * - is_admin: Flag for admin user status. Will be true when the current user
    *   is an administrator.
    *
    * @see template_preprocess_node()
    *
    * @todo Remove the id attribute (or make it a class), because if that gets
    *   rendered twice on a page this is invalid CSS for example: two lists
    *   in different view modes.
    *
    * @ingroup themeable
    */
    #}
    <article{{ attributes }}>

    {{ title_prefix }}
    {% if not page %}
        <h2{{ title_attributes }}>
        <a href="{{ url }}" rel="bookmark">{{ label }}</a>
        </h2>
    {% endif %}
    {{ title_suffix }}

    {% if display_submitted %}
        <footer>
        {{ author_picture }}
        <div{{ author_attributes }}>
            {% trans %}Submitted by {{ author_name }} on {{ date }}{% endtrans %}
            {{ metadata }}
        </div>
        </footer>
    {% endif %}

    <div{{ content_attributes }}>
        {{ content }}
    </div>

    </article>

Blocks
-----=

Pattern: ``block--[module|-delta]].html.twig``
Base template: ``block.html.twig`` (base location: ``core/modules/block/templates/block.html.twig``)

1. ``block--module--delta.html.twig``
2. ``block--module.html.twig``
3. ``block.html.twig``

"module" being the name of the module and "delta", the internal id assigned to the block by the module.

For example, "block--block--1.html.twig" would be used for the first user-submitted block added from the block administration screen since it was created by the block module with the id of 1. Region-specific block templates are not available in Drupal 8.

If you had a block created by a custom module called "custom" and a delta of "my-block", the theme hook suggestion would be called "block--custom--my-block.html.twig."

Also one more example with Views, if you have a block created by views with a view name "front_news" and display id "block_1" then the theme hook suggestion would be: block--views-block--front-news-block-1.html.twig (notice, when you have underscores in a display id or in a view name - you have to transform them in to a single dash)

Be aware that module names are case sensitive in this context. For instance if your module is called 'MyModule', the most general theme hook suggestion for this module would be "block--MyModule.html.twig."

See the `block.html.twig API documentation <https://api.drupal.org/api/drupal/core!modules!block!templates!block.html.twig/8>`_.

Related topics
--------------

- `Theme system overview <https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Render%21theme.api.php/group/themeable/8.2.x>`_: Functions and templates for the user interface that themes can override.

