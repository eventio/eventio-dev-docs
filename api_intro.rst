API Introduction
****************

For advanced access of various data and functionality of Eventio.com,
**HTTP API** can be used. This section includes general information what
is needed to access the Eventio API.

Endpoints & API Versions
========================

HTTP API endpoint URLs start with a common prefix
``https://eventio.com/api/2013-01-01/``. The API version number (the date)
in the URL may change if major backwards incompatible changes are implemented.
Note that request parameters and JSON fields in responses can be added to
existing endpoints.

.. warning::

    The current API version is at its beta and changes occur frequently. Please
    coordinate with Eventio Customer Support if you intend to use API in
    production.

API Keys
========

Each application must authenticate themselves with Eventio.com with an **API key**
and a **shared secret**. The authentication is done by means of
**HTTP Basic Authentication** at every request: API key is provided as the
user name, shared secret as the password.

Each event organizer manages its own API keys through the account settings page
in Eventio. An API key is therefore assigned to a certain organizer and
limited only to certain organizer's data. There is no limits how many API keys
one organizer may have.

When a new API key is created, a random string called **shared secret** is generated
and displayed to the API key creator. **The shared secret is visible only upon
creation** and cannot be recovered later.

If authentication fails, API endpoint replies with standard ``401 Unauthorized``
HTTP response.

Data Formats
============

HTTP requests from the application can be usually sent with proper HTTP POST
parameters in ``application/x-www-form-urlencoded`` format. When more complex
data structure is required by the endpoint, the data can given as JSON.

HTTP responses from Eventio API endpoint are usually JSON.

Request Throttling
==================

Eventio limits the amount of requests that can be sent to the API endpoints.
If an application exceeds the request limits, ``429 Too Many Requests`` response
is given.