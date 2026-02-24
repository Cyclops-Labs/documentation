================
Define SKU
================

An SKU (AKA Stock Keeping Unit) for us is a type of resource, they need to be defined first and should represent all types reported by Cyclops collectors, or in data pushed from the external sources. 
Examples of such are: server, disk, IP-address, etc. They should reflect precisely all resource types that are supposed to be billed.
For defining one you need to provide: id, name, and unit.

Below is the example of bash script that uploads the SKUs::

    #!/bin/bash

    SERVER="https://<deployment-url>/planmanagerAPI"
    API_KEY="<key>"
    API_VERSION="v1.0"

    # load the skus
    curl --silent -H "X-API-Key: ${API_KEY}" -H "Content-Type: application/json" "${SERVER}/api/${API_VERSION}/sku" -X POST -d '{ "id":  "1", "name": "cpu001ram001", "unit": "Instance" }'
    curl --silent -H "X-API-Key: ${API_KEY}" -H "Content-Type: application/json" "${SERVER}/api/${API_VERSION}/sku" -X POST -d '{ "id":  "2", "name": "cpu001ram002", "unit": "Instance" }'
    curl --silent -H "X-API-Key: ${API_KEY}" -H "Content-Type: application/json" "${SERVER}/api/${API_VERSION}/sku" -X POST -d '{ "id":  "3", "name": "cpu002ram004", "unit": "Instance" }'
    curl --silent -H "X-API-Key: ${API_KEY}" -H "Content-Type: application/json" "${SERVER}/api/${API_VERSION}/sku" -X POST -d '{ "id":  "4", "name": "cpu004ram008", "unit": "Instance" }'
    # continue with all SKUs