================
Metrics model
================

The data model for *usage-based* reporting is:

.. code-block:: json

    {
        "Account": "string",
        "Metadata": "JSON",
        "ResourceType": "string",
        "ResourceId": string,
        "Time": "string",
        "Unit": "string",
        "Usage": "floating-point"
    }

- **Account** – Refers to the billed user account ID. It is used for grouping billing data per billable user. It should be a unique identifier defined externally to the Cyclops system.
- **Metadata** – Additional data provided as JSON that may be useful for further processing.
- **ResourceType** – Defined when creating SKUs. This corresponds to the SKU name.
- **ResourceId** - ID of the reported resource. It does not needs to hold a value, but can be set for easier data handling/aggregation later on.
- **Time** – Timestamp indicating when the usage record was created. Must be in *Unix timestamp* format.
- **Unit** – The unit of the **Usage** field (for example, "GB").
- **Usage** – The measured value (for example, disk size), expressed in the unit defined by **Unit**.

Requirements for the ``Time`` field:

- Must be a Unix timestamp (seconds since epoch)
- Must be expressed in UTC
- Must represent the actual measurement time

``Metadata field`` should contain the data field used for unique resource recognition. For example:

- S3 storage metadata: ``{ "region": "<deployment region>", "bucket": "<bucket name>" }``
- HEAppE metadata: ``{ "account": "<account string>", "resourceID": "<cluster node ID>", "resourceName": "<cluster node name>" }``

Also, in order to have "fast mode" aggregation enabled, medatada should contain field "UDRMode": "sum". This will make these metrics be aggregated in 5 minutes intervals. 