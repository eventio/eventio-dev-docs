Eventio Connect for WordPress
*****************************

Eventio Connect for WordPress is a plugin that can be used to integrate Eventio
to a WordPress website.

Installation
============

 * Request the plugin file from Eventio's customer support
 * Install the plugin to your WordPress.
 * In WP admin panel, see the plugin settings under Plugins > Eventio Connect.
   Add your Eventio's webservice URL to the appropriate field.

Shortcodes
==========

The plugin provides a couple of different shortcodes that you can place into
your WP pages.

[eventio_event_list]
--------------------

Shortcode ``[eventio_event_list]`` adds a list of all your upcoming events.

[eventio_event_list_by_name]
----------------------------

Shortcode ``[eventio_event_list_by_name]`` adds a list of events that match
the given WP page title. If the page title cannot be used or does not match
the actual event name, you can also provide the name as the shortcode
attribute ``by_name``:

``[eventio_event_list_by_name by_name="Traktoriralli"]`` would list all events named as "Traktoriralli", no matter what is the page title.

[eventio_product_list]
----------------------

Shortcode ``[eventio_product_list]`` adds a list of all your non-event related products, like
serial cards or merchandising.