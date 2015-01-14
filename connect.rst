Eventio Connect
***************

Eventio Connect is the most easiest way to integrate Eventio to any website.
Different widgets, functions and information can be embedded into websites
conveniently by adding short Javascript and HTML code snippets to
intended locations of a webpage.

.. note::

    Using Eventio Connect does not require API Keys.

Add The Site Snippet
====================

The first task is to add a so called **site snippet** inside the ``<head>`` tag of
your site. Most propably you want to add the site snippet to your website's
template so it's automatically added on every page.

.. code-block:: html

    <script>
    (function(d, s, id) {
        var js, fjs = d.getElementsByTagName(s)[0];
        if (d.getElementById(id))
            return;
        js = d.createElement(s);
        js.id = id;
        js.src = '//d37z53xi4tkke2.cloudfront.net/2013-07-01/eventio-connect.js';
        fjs.parentNode.insertBefore(js, fjs);
    }(document, 'script', 'eventio-connect-js'));
    </script>

Add A Widget Tag
================

To place the actual widget, you should place the proper **widget tag** to
the intended position in your HTML source. The widget snippet is actually
**a ``<div>``** tag with a class ``eventio_frame`` and some special attributes.

Widget Tag Attributes
---------------------

``class`` must be present and must include ``eventio_frame``.

``data-url`` is the actual URL of the widget. There are a few ready widgets that
can be used without further configuration (or configured in the query string).
More advanced widgets and configuration can be done through the Eventio
administration console.

``data-initial-height`` can be used to set an initial height for the ``<iframe>``
to be loaded. The ``iframe`` will adjust it's height to the actual contents
but while the widget content is loading, the height normally defaults to browser's
default height (150 px) that might be unnecessary large.

Example
-------

.. code-block:: html

    <div class="eventio_frame" data-url="http://liput.traktoriralli.fi/fi/events/widget/ebw/5297c3da0071765d218b456a/w" />

Widgets in Practice
-------------------

When a page including some widgets is loaded, the Javascript in the site snippet
reads all tags on the page that match ``class="eventio_frame"``.
A new ``<iframe>`` is loaded inside each tag with
the contents provided in ``data-url`` attribute.

CMS Plugins
===========

There are existing plugins available for popular content management systems. The
plugins take care of adding required snippets.