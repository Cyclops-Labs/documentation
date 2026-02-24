================
Building Plan
================

API sequence
#############

Plan is an object that links **customers** and **sku prices**. Its presence is crucial for the billing cycle to succeed.
Also this mechanism allows to perform different billing logic per customer.
To create the plan, following fields needs to be provided:

- **ID** - plan ID (integer)
- **Name** - plan name (string)
- **OfferedEndDate** - date when the plan should stop being used for billing (string)
- **OfferedStartDate** - date when the plan should start being used for billing (string)
- **SkuPrices** - optional filed of SKU prices, can be set to *null*

Below is the example of bash script that uploads the SKUs::

    #!/bin/bash

    SERVER="https://<deployment-url>/planmanagerAPI"
    API_KEY="<key>"
    API_VERSION="v1.0"

    # load the billing plans
    curl --silent -H "X-API-Key: ${API_KEY}" -H "Content-Type: application/json" "${SERVER}/api/${API_VERSION}/plan" -X POST -d '{ "ID":  "1", "Name": "default", "OfferedEndDate": "2099-12-31", "OfferedStartDate": "2026-01-01", "SkuPrices": null }'


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