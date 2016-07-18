.. highlight:: js

.. _calls-userblockrfid-docs:

User Block RFID
===============

Request
-------

``"user-block-rfid"`` identifies the call as a user-block-rfid call.

Fields
~~~~~~

user
    This field identifies the customer (object).

    identifier-type
        How to identify the user (string).

        The identifier-type can be one of:

        * ``"evco-id"``
        * ``"rfid"``
        * ``"username"``

    identifier
        The identifier is something that uniquely identifies the customer,
        depending on the identifier-type (string).

    token (optional)
        A token can be used to authenticate the user (string).

        For example: if the identifier type is username and the identifier is the user's username,
        then token is used for authentication instead of a password.

rfid
    The RFID (UID) of the user that should be blocked (string).

    .. important:: - An RFID must have a length of 8, 14 or 20 characters.
                     If necessary, the RFID must be zero-padded on the left.

                   - It should be read from left to right using big-endian format.

                   - All characters must be upper-case.

Response
--------

Fields
~~~~~~

success
   Whether or not the call was a success (boolean).

Status codes
~~~~~~~~~~~~
200 OK
  Successfull
401 Unauthorized
  The token, username or identifier type were incorrect
404
  The RFID for that user could not be found

Examples
--------

Request::

    {
        "user-block-rfid": {
            "user": {
                "identifier-type": "username",
                "identifier": "john",
                "token": "b3853b6d910849f3b4392555b8acb984"
            },
            "rfid": "12345678ABCDEF"
        }
    }

Response::

    {
        "user-block-rfid": {
            "success": true
        }
    }
