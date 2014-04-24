Send SMS
********

+---------------+----------------------------------------------------+
| Endpoint      | ``https://eventio.com/api/2013-01-01/sms/_send``   |
+---------------+----------------------------------------------------+
| Method        | POST                                               |
+---------------+----------------------------------------------------+

This endpoint is used to send SMS messages via Eventio.

.. note::

    Sent messages are billed according to Eventio's price list and contract.

Request Parameters
==================

Parameters are given as **HTTP POST** field values.

+-------------------+----------------------------------------------------------------------+
| ``to``            | Recipient number(s). Mulitple numbers can be given as a string,      |
|                   | delimited with a comma ``,`` or with multiple ``to[]`` parameters.   |
|                   | Use international format +358401234567.                              |
+-------------------+----------------------------------------------------------------------+
| ``text``          | Actual message body.                                                 |
+-------------------+----------------------------------------------------------------------+
| ``priorityclass`` | ``n`` for normal priority (default), ``p`` for prioritized message.  |
+-------------------+----------------------------------------------------------------------+
| ``sender``        | Sender name (max 11 characters, only A-Z or a-z). This is shown as   |
|                   | the message sender if the message class and route allows it.         |
+-------------------+----------------------------------------------------------------------+

Response
========

Response is given as JSON.

+-----------------------+----------------------------------------------------------------+
| ``ok``                | ``true``                                                       |
+-----------------------+----------------------------------------------------------------+
| ``message_id_list``   | JSON hash of recipient numbers and corresponding message IDs.  |
|                       | Note: this information is given only if there are <= 10        |
|                       | recipients.                                                    |
+-----------------------+----------------------------------------------------------------+
| ``message_count``     | In how many actual SMSes the actual message is sent.           |
+-----------------------+----------------------------------------------------------------+

Notes
=====

* Eventio does a sanity check on the given recipient numbers, removes duplicates and silently
  skips invalid numbers that cannot be parsed to an international format.
* Depending on the length of the SMS body (``text``), one message can be considered
  as multiple messages (>160 characters) and billed accordingly.