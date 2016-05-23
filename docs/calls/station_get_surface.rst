.. highlight:: js

.. _calls-stationgetsurface-docs:

Station Get Surface
===================

Request
-------

``"station-get-surface"`` identifies the call as a station-get-surface call.

Define a rectangle on a map by providing two corners:

    1. Minimum latitude and longitude
    2. Maximum latitude and longitude

Fields
~~~~~~

min-lat
    Minimum latitude of the area you are querying (float).
max-lat
    Maximum latitude of the area you are querying (float).
min-long
    Minimum longitude of the area you are querying (float).
max-long
    Maximum longitude of the area you are querying (float).
filters
    An object to filter the response (object).

    Omit any filter you do not want to use in the request.

    Available Filters:

    excludes
        A list of station IDs to exclude from the result (array of integers).
    company-types
        A list of owner types of the charging stations (array of strings).

        E.g. ``"hotel"``.
    connector-types
        A list of connector types to filter for (array of strings).

        Allowed types are:

        * ``"Type2"``
        * ``"Combo"``
        * ``"Chademo"``
        * ``"Schuko"``
        * ``"Type3"``
        * ``"CeeBlue"``
        * ``"3PinSquare"``
        * ``"Type1"``
        * ``"CeeRed"``
        * ``"Cee2Poles"``
        * ``"Tesla"``
        * ``"Scame"``
        * ``"Nema5"``
        * ``"CeePlus"``
        * ``"T13"``
        * ``"T15"``
        * ``"T23"``
        * ``"Marechal"``

    connector-speeds-greater
        Minimum value for charging speed in kW (float).
    connector-speeds-less
        Maximum value for charging speed in kw (float).
    operator-ids
        List of charging station operator ids (array of integers).
    payable
        List of payment methods that should be available (array of strings).

        Available are:

        * ``"app"``
        * ``"rfid"``

Response
--------

Fields
~~~~~~


stations
    An array of charging stations (objects).

    id
        The reponder's ID of the station (integer).

        Use this ID in the excludes filter (see request) or to get more details.
        See also :ref:`calls-stationgetbyids-docs`.
    name
        The name of the station, human readable (string).
    latitude
        Latitude of this station (float).
    longitude
        Longitude of this station (float).
    dynamic-status-summary
        Whether the station has available connectors (string).

        Can be one of:

        * ``"AVAILABLE"``
        * ``"OCCUPIED"``
        * ``"OFFLINE"``
        * ``null``

    owner-type
        The type of the company (string or ``null``).

        E.g. "hotel".
    last-static-change
        The last time the station was updated (string).

        The date/time format is RFC3339 (``Y-m-d\TH:i:sP``).

Status codes
~~~~~~~~~~~~

200 OK
    The request was processed successfully.

Examples
--------

Request::

    {
        "station-get-surface": {
            "min-lat": 0,
            "max-lat": 45,
            "min-long": 30,
            "max-long": 40,
            "filters": {
                "excludes": [
                    11131
                ],
                "company-types": [
                    "hotel"
                ],
                "connector-types": [
                    "Type2"
                ],
                "connector-speeds-greater": 3,
                "connector-speeds-less": 100,
                "operator-ids": [
                    122,
                    32
                ],
                "payable": [
                    "app",
                    "rfid"
                ]
            }
        }
    }

Response::

    {
        "stations": [
            {
                "id": 1169,
                "name": "Marktparkhaus am Südwall",
                "latitude": 51.516123,
                "longitude": 6.322554,
                "dynamic_status_summary": null,
                "owner_type": null
            },
            {
                "id": 1622,
                "name": "Markt",
                "latitude": 51.51599,
                "longitude": 6.322551,
                "dynamic_status_summary": null,
                "owner_type": null
            }
        ]
    }
