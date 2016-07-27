.. highlight:: js

.. _calls-connectorpoststatus-docs:

Connector Post Status
=====================

Request
-------

``"connector-post-status"`` identifies the call as a status update call.

Fields
~~~~~~

connector-id
    The EVSE ID of the connectors (string).
    All connectors with the given connector-id will be updated.
    See also :ref:`EVSE <glossary-evse>`.
status
    One of the following strings:

    * ``"Available"``
    * ``"Occupied"``
    * ``"Offline"``
    * ``"Reserved"``
    * ``"Unknown"``

partner-identifier
    The partner identifier of the partner that owns the connector (string).
    See also :ref:`partner identifier <glossary-partner-identifier>`

Response
--------

Fields
~~~~~~

success
    Whether or not the call was a success (boolean)

Status codes
~~~~~~~~~~~~

200
    All went well
404
    The connector or the status were not found
422
    The connector could not be identified uniquely

Examples
--------

Request::

    {
        "connector-post-status": {
            "connector-id": "DE*8PS*E123456",
            "partner-identifier": "123456-123456-abcdef-abc123-456def",
            "status": "Available"
        }
    }

Response::

    {
        "connector-post-status": {
            "success": true
        }
    }
