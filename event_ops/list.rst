Retrieve Event List
*******************

+---------------+----------------------------------------------------+
| Endpoint      | ``https://eventio.com/api/2013-01-01/events/list`` |
+---------------+----------------------------------------------------+
| Method        | GET                                                |
+---------------+----------------------------------------------------+

This endpoint is used to retrieve all confirmed events from Eventio.

Request Parameters
==================

Parameters are given as **query string values**.

+---------------+----------------------------------------------------------------------+
| ``after``     | List only events starting after the given time. Enter the value in   |
|               | `ISO 8601 <http://en.wikipedia.org/wiki/ISO_8601>` format.           |
|               | Defaults to current date.                                            |
+---------------+----------------------------------------------------------------------+
| ``before``    | List only events starting before the given time. Enter the value in  |
|               | `ISO 8601 <http://en.wikipedia.org/wiki/ISO_8601>` format.           |
|               | Defaults to the current date + 365 days.                             |
+---------------+----------------------------------------------------------------------+
| ``offset``    | Skip given amount of results from the beginning. Useful when looping |
|               | through multiple pages. (see limit)                                  |
+---------------+----------------------------------------------------------------------+
| ``limit``     | Return only given amount of results. Defaults to 100 that is also    |
|               | the maximum.                                                         |
+---------------+----------------------------------------------------------------------+

Response
========

This endpoint returns a JSON **array** of events. Events are given in chronological
order, sorted by the start date.

+------------------+-----------------------------------------------------------------------+
| ``id``          | Internal Event ID (24-digit hex)                                       |
+------------------+-----------------------------------------------------------------------+
| ``title``        | Public name of the event.                                             |
+------------------+-----------------------------------------------------------------------+
| ``begins``       | Timestamp of the event start time in                                  |
|                  | `ISO 8601 <http://en.wikipedia.org/wiki/ISO_8601>` format             |
+------------------+-----------------------------------------------------------------------+
| ``ends``         | Timestamp of the event end time in                                    |
|                  | `ISO 8601 <http://en.wikipedia.org/wiki/ISO_8601>` format.            |
|                  | This information is given only if entered by the organizer.           |
+------------------+-----------------------------------------------------------------------+
| ``time_info``    | Arbitrary information about the time of the event, given by the       |
|                  | organizer. In case this field is given, this information should be    |
|                  | shown for customers instead of exact date and time                    |
|                  | (``begins`` and ``ends`` fields).                                     |
+------------------+-----------------------------------------------------------------------+
| ``status``       | Status of the event:                                                  |
|                  |                                                                       |
|                  | * ``confirmed`` = The event will be organized.                        |
|                  | * ``ongoing``   = The event is currently going on.                    |
|                  | * ``finished``  = The event is already ended.                         |
|                  |                                                                       |
+------------------+-----------------------------------------------------------------------+
| ``location``     | Nested JSON object about the event location if known.                 |
|                  |                                                                       |
|                  | ``id``: Internal ID of the location (24-digit hex) if applicable.     |
|                  | ``title``: Public name of the location.                               |
|                  |                                                                       |
+------------------+-----------------------------------------------------------------------+
| ``price_info``   | Price information of the event. Note: this field is a string with     |
|                  | currency symbol and possible VAT information.                         |
+------------------+-----------------------------------------------------------------------+
| ``availability`` | Nested sales availability information for the event.                  |
|                  |                                                                       |
|                  | ``available``: Is the ticket sales / registration open? true or false |
|                  | ``info``: Arbitrary information about closed sales.                   |
|                  | ``buybox_popup_url``: URL of the sales screen, if available.          |
+------------------+-----------------------------------------------------------------------+
| ``description``  | Nested JSON object of description / additional information about the  |
|                  | event.                                                                |
|                  |                                                                       |
|                  | ``short``: Short description (a sentence or two), text only.          |
|                  | ``long``: Long description (multiple paragraphs), may contain html.   |
|                  |                                                                       |
+------------------+-----------------------------------------------------------------------+

Availability & Sales screen
===========================

In case the event is available for customers (ticket sales or registration), a nested JSON
field ``availability.buybox_popup_url`` exists on the results. The client application
may use this URL to open a popup window for the customer to show further information
about available tickets.

It's possible that the event is not currently available for the customers. In this case,
the organizer may provide further details in the ``availability.info`` field. This information
should be shown for the customer.