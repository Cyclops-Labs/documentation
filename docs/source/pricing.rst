==================
Define SKU pricing
==================

API sequence
#############

For creating a SKU Price you need the following values: skuid, skuname, unitprice, unit, and planid.

- **skuid** - SKU ID, as defined before for given SKU during it creation (integer)
- **skuname** - SKU name, also as defined before (string)
- **unitprice** - *per second* price of SKU (floating point)
- **unit** - unit used for billing (string)
- **planid** - ID of a created billing plan that defined SKU price should by linked to (integer)
- **TimeUnit** - unit of time used for billing. Should be set to "second" (string)

*The skuid and name have to be the exact same from the SKU you want to add a price and the same goes for the planid.* 

Below is the example of bash script that sets the SKU price::

    #!/bin/bash

    SERVER="https://<deployment-url>/planmanagerAPI"
    API_KEY="<key>"
    API_VERSION="v1.0"

    # load the SKU prices
    curl --silent -H "X-API-Key: ${API_KEY}" -H "Content-Type: application/json" "${SERVER}/api/${API_VERSION}/sku/price" -X POST -d '{ "skuid": "13", "skuname": "cpu008ram008", "unitprice": 0.000060882800608, "unit": "Instance", "planid": "1", "TimeUnit": "second" }'

API responses
#############

201 Created
***********

**Description:** Item successfully created.

**Response body:**

.. code-block:: json

    {
        "Link": "string",
        "ID": "string",
        "Message": "string"
    }

400 Bad Request
***************

**Description:** Invalid input data.

409 Conflict
************

**Description:** Item already exists.

**Response body:**

.. code-block:: json

    {
        "errorString": "string"
    }

500 Unexpected error
********************

**Description:** Unexpected server error occured.

**Response body:**

.. code-block:: json

    {
        "errorString": "string"
    }