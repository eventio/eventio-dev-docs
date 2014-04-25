Retrieve Order List
*******************

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

+---------------+----------------------------------------------------------------------+
| ``after``     | List only orders created after the given time. Enter value in        |
|               | `ISO 8601 <http://en.wikipedia.org/wiki/ISO_8601>` format.           |
|               | If value is not given, all orders are listed.                        |
+---------------+----------------------------------------------------------------------+
| ``before``    | List only orders created before the given time. Enter value in       |
|               | `ISO 8601 <http://en.wikipedia.org/wiki/ISO_8601>` format.           |
|               | If value is not given, all orders are listed until the current time. |
+---------------+----------------------------------------------------------------------+
| ``offset``    | Skip given amount of results from the beginning. Useful when looping |
|               | through multiple pages. (see limit)                                  |
+---------------+----------------------------------------------------------------------+
| ``limit``     | Return only given amount of results. Defaults to 100 that is also    |
|               | the maximum.                                                         |
+---------------+----------------------------------------------------------------------+
| ``cancelled`` | ``1`` = Include also cancelled orders in results. Defaults to false. |
+---------------+----------------------------------------------------------------------+

Response
========

This endpoint returns a JSON **array** of order records. See format of one
order record from from :doc:`info`.

Notes
=====

* If an order is deleted, it does no more exist on the results. Use ``id`` to track
  if certain order still exists. To confirm the deletion, you can make a request
  to the :doc:`order's info endpoint <info>`. It will respond with ``404 Not Found``
  for deleted orders.