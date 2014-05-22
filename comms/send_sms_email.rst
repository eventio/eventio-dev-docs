Send SMS over Email
*******************

In addition to HTTP Request, SMS messages can be sent also by delivering a
JSON formatted e-mail message to an e-mail address.

.. note::

    Sent messages are billed according to Eventio's price list and contract.

To:
===

The e-mail message should be sent to ``<recipient>@sms.eventio.com``, where
``<recipient>`` is the actual GSM number. 

Subject
=======

The e-mail message subject is ignored.

Body
====

The message body should contain a JSON formatted string with following fields:

+----------+---------------------------------------------------------------------+
| ``body`` | Actual SMS message body.                                            |
+----------+---------------------------------------------------------------------+
| ``api``  | JSON object with API credentials, where ``key`` is the API key and  |
|          | ``pwd`` is the shared secret.                                       |
+----------+---------------------------------------------------------------------+
| ``to``   | (optional) JSON array of recipient numbers if same message is to be |
|          | sent to multiple recipients. Overrides the recipient number         |
|          | given in the e-mail message's To: field.                            |
+----------+---------------------------------------------------------------------+

Examples
========

To send an SMS "Test message" to number +358403110565.

+----------+-----------------------------------------------------------------------------+
| **To:**  | +358403110565@sms.eventio.com                                               |
+----------+-----------------------------------------------------------------------------+
| **Body** | ``{"body":"Test message","api": {"key": "<API KEY>", "pwd": "<SECRET>"}}``  |
+----------+-----------------------------------------------------------------------------+

Notes
=====

* Eventio does a sanity check on the given recipient numbers, removes duplicates and silently
  skips invalid numbers that cannot be parsed to an international format.
* Depending on the length of the SMS body (``text``), one message can be considered
  as multiple messages (>160 characters) and billed accordingly.