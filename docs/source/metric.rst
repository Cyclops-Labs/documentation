================
Metrics model
================

The data model for *usage-based* reporting is:

.. code-block:: json

    {
        "Account": "string",
        "Metadata": "JSON",
        "ResourceType": "string",
        "Time": "string",
        "Unit": "string",
        "Usage": "floating-point"
    }

- **Account** – Refers to the billed user account ID. It is used for grouping billing data per billable user. It should be a unique identifier defined externally to the Cyclops system.
- **Metadata** – Additional data provided as JSON that may be useful for further processing. For example, the "region" where the billed resource is deployed or the resource name/ID.
- **ResourceType** – Defined when creating SKUs. This corresponds to the SKU name.
- **Time** – Timestamp indicating when the usage record was created. Must be in *Unix timestamp* format.
- **Unit** – The unit of the **Usage** field (for example, "GB").
- **Usage** – The measured value (for example, disk size), expressed in the unit defined by **Unit**.

Requirements for the ``Time`` field:

- Must be a Unix timestamp (seconds since epoch)
- Must be expressed in UTC
- Must represent the actual measurement time