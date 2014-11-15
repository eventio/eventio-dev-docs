Download PDF Tickets
********************

+---------------+-----------------------------------------------------------------+
| Endpoint      | ``https://eventio.com/api/2013-01-01/orders/tickets/_download`` |
+---------------+-----------------------------------------------------------------+
| Method        | POST                                                            |
+---------------+-----------------------------------------------------------------+

This endpoint is used to download the PDF tickets of an order. In case of tickets are not
issued, this action also generates the tickets to the system. If the tickets are
already issued before, this will return the tickets. If an order contains more than
one issue groups, the most recent issue group is returned.


Request Parameters
==================

Parameters are given as **HTTP POST request values**.

+-----------------+----------------------------------------------------------------------+
| ``order``       | The order must be identified with its ID (24 hex-digits) or number   |
|                 | (two capital letters + three or more digits)                         |
+-----------------+----------------------------------------------------------------------+
| ``only_person`` | If you want tickets only for a certain person, give the person id    |
                  | or e-mail address.                                                   |
+-----------------+----------------------------------------------------------------------+
| ``media``       | The media type for the tickets. Possible values:                     |
|                 |                                                                      |
|                 | * ``a4_pdf_eticket`` for self-printable tickets                      |
|                 | * ``a4_pdf_bulk`` for A4 bulk printing                               |
|                 | * ``thermo`` for thermal printing                                    |
|                 |                                                                      |
+-----------------+----------------------------------------------------------------------+

Response
========

JSON object.

+-------------------+-----------------------------------------------------------------+
| ``pdf``           | The PDF file in base64-encoded format                           |
+-------------------+-----------------------------------------------------------------+
| ``issuegroup_id`` | The ID of the ticket issue group.                               |
+-------------------+-----------------------------------------------------------------+
| ``issued``        | Timestamp of the ticket issuance in                             |
|                   | `ISO 8601 <http://en.wikipedia.org/wiki/ISO_8601>` format       |
+-------------------+-----------------------------------------------------------------+
