Retrieve Orders
***************

+---------------+----------------------------------------------------+
| Endpoint      | ``https://eventio.com/api/2013-01-01/orders/list`` |
+---------------+----------------------------------------------------+
| Method        | GET                                                |
+---------------+----------------------------------------------------+

This endpoint is used to retrieve all non-deleted orders from Eventio. Note
that the result contains also tentative and unpaid orders until they are
automatically or manually deleted.

Request Parameters
==================

Parameters are given as **query string values**.

+------------+----------------------------------------------------------------------+
| ``after``  | List only orders created after the given time. Enter value in        |
|            | `ISO 8601 <http://en.wikipedia.org/wiki/ISO_8601>` format.           |
|            | If value is not given, all orders are listed.                        |
+------------+----------------------------------------------------------------------+
| ``before`` | List only orders created before the given time. Enter value in       |
|            | `ISO 8601 <http://en.wikipedia.org/wiki/ISO_8601>` format.           |
|            | If value is not given, all orders are listed until the current time. |
+------------+----------------------------------------------------------------------+
| ``offset`` | Skip given amount of results from the beginning. Useful when looping |
|            | through multiple pages. (see limit)                                  |
+------------+----------------------------------------------------------------------+
| ``limit``  | Return only given amount of results. Defaults to 100 that is also    |
|            | the maximum.                                                         |
+------------+----------------------------------------------------------------------+

Response
========

JSON array of order records or an empty array.

+--------------+----------------------------------------------------------------------+
| ``id``       | Internal Order ID (24-digit hex)                                     |
+--------------+----------------------------------------------------------------------+
| ``order_nr`` | Human-readable order number for accepted orders. Numbers are not     |
|              | re-used but are unique only for an organizer. Integer value.         |
+--------------+----------------------------------------------------------------------+
| ``time``     | Timestamp of the order, in                                           |
|              | `ISO 8601 <http://en.wikipedia.org/wiki/ISO_8601>` format            |
+--------------+----------------------------------------------------------------------+
| ``customer`` | Nested document of customer details. See below.                      |
+--------------+----------------------------------------------------------------------+
| ``items``    | Array of items (= lines) in the current order. See below.            |
+--------------+----------------------------------------------------------------------+

Customer Info
-------------

Each order record contains the following customer sub-document, where applicable.

+----------------+----------------------------------------------------------------------+
| ``type``       | ``p`` = person, ``o`` = organization                                 |
+----------------+----------------------------------------------------------------------+
| ``name``       | Name of the organization (if ``type``=``o``)                         |
+----------------+----------------------------------------------------------------------+
| ``firstname``  | First name of the customer (if ``type``=``p``)                       |
+----------------+----------------------------------------------------------------------+
| ``lastname``   | Last (family) name of the customer (if ``type``=``p``)               |
+----------------+----------------------------------------------------------------------+
| ``address``    | Postal address line / P.O. Box                                       |
+----------------+----------------------------------------------------------------------+
| ``postalcode`` | Postal code                                                          |
+----------------+----------------------------------------------------------------------+
| ``city``       | Name of the city                                                     |
+----------------+----------------------------------------------------------------------+
| ``country``    | `ISO 3166 <http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2>`_        |
|                | country code of the customer.                                        |
+----------------+----------------------------------------------------------------------+
| ``phone``      | Phone number (in the international format)                           |
+----------------+----------------------------------------------------------------------+
| ``email``      | Email address of the customer.                                       |
+----------------+----------------------------------------------------------------------+
| ``org_id``     | Internal organization ID of the customer.                            |
+----------------+----------------------------------------------------------------------+
| ``person_id``  | Internal person ID of the customer.                                  |
+----------------+----------------------------------------------------------------------+
| ``id``         | Internal ID of the customer.                                         |
+----------------+----------------------------------------------------------------------+

Order Item details
------------------

An order contains usually one or more order items, i.e. actual products purchased.
Active items are listed as a JSON array in ``items`` field and follow the format below.

+-------------------+----------------------------------------------------------------------+
| ``amount``        | Ordered amount (ticket count etc.)                                   |
+-------------------+----------------------------------------------------------------------+
| ``status``        | Status of the item: ``tentative`` or ``confirmed``.                  |
+-------------------+----------------------------------------------------------------------+
| **``product``**   | Subdocument of product information. See actual fields below.         |
+-------------------+----------------------------------------------------------------------+
| ``product.id``    | Internal product ID                                                  |
+-------------------+----------------------------------------------------------------------+
| ``product.title`` | Title (name) of the product.                                         |
+-------------------+----------------------------------------------------------------------+
| **``event``**     | Subdocument of event information. See actual fields below.           |
+-------------------+----------------------------------------------------------------------+
| ``event.id``      | Internal event ID                                                    |
+-------------------+----------------------------------------------------------------------+
| ``event.time``    | Time of the event in ISO 8601 format. Pay attention to the timezone. |
+-------------------+----------------------------------------------------------------------+
| ``event.title``   | Title (name) of the event.                                           |
+-------------------+----------------------------------------------------------------------+

Notes
=====

* If an order is cancelled, it will no more exist on the results. Use ``id`` to track
  if certain order still exists.
* The item status depends on the organizer's configuration how purchases are confirmed. The
  rule of a thumb is that when the item is ``confirmed`` it's paid and in case of ticket
  products, tickets are issued.
* If an event is rescheduled, item's ``event.id`` remains the same even ``event.time`` changes.