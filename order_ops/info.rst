Retrieve Order Info
*******************

+---------------+--------------------------------------------------------+
| Endpoint      | ``https://eventio.com/api/2013-01-01/orders/info/:id`` |
+---------------+--------------------------------------------------------+
| Method        | GET                                                    |
+---------------+--------------------------------------------------------+

This endpoint is used to retrieve details of **one order**.

To list all orders and their IDs, read :doc:`list`.

Request Parameters
==================

The order is identified in the URL's ``:id`` placeholder. Replace it with
the internal 24-digit hex ID of the order.

There are no further parameters that can be provided to the endpoint.

Response
========

JSON object of the order in question.

+--------------+----------------------------------------------------------------------+
| ``id``       | Internal Order ID (24-digit hex)                                     |
+--------------+----------------------------------------------------------------------+
| ``order_nr`` | Human-readable order number for accepted orders. Numbers are not     |
|              | re-used but are unique only for an organizer. Integer value.         |
+--------------+----------------------------------------------------------------------+
| ``time``     | Timestamp of the order, in                                           |
|              | `ISO 8601 <http://en.wikipedia.org/wiki/ISO_8601>` format            |
+--------------+----------------------------------------------------------------------+
| ``status``   | Status of the whole order. Possible values:                          |
|              |                                                                      |
|              | * ``draft`` = Order is in draft mode.                                |
|              | * ``active`` = Order is currently active.                            |
|              | * ``cancelled`` = Order is cancelled.                                |
|              |                                                                      |
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

* Order can be fully deleted whichafter it does not exists (``404 Not Found`` is returned)
  at all. Cancelled orders have status ``cancelled``.
* The item status depends on the organizer's configuration how purchases are confirmed. The
  rule of a thumb is that when the item is ``confirmed`` it's paid and in case of ticket
  products, tickets are issued.
* If an event is rescheduled, item's ``event.id`` remains the same even ``event.time`` changes.