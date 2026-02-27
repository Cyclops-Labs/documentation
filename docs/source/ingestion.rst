================
Sending Data
================

Usage Data
##########

The data structure defined in the *Metrics Model* page must be published to the Kafka service.

Each Kafka message represents **a single usage record for a single resource**.

Messages are transmitted individually (one resource per message), not as aggregated batches.

Message Semantics
-----------------

Each published message must:

- Represent exactly one resource.
- Reflect the current measured state of that resource.
- Contain a valid ``Time`` field (Unix timestamp, UTC).
- Be encoded as UTF-8 JSON.

Duplicate usage records must not be produced by the reporting system.

A usage record is uniquely identified by the following fields:

- ``Account``
- ``ResourceId``
- ``ResourceType``
- ``Time``

Billing Time Semantics
----------------------

Billing calculations are based strictly on the timestamp provided in the ``Time`` field.

The system uses **event time**, not Kafka ingestion time.

Incorrect timestamps will directly impact billing accuracy.

Kafka Configuration
--------------------

- **Brokers**: Configurable list of Kafka broker addresses
- **Topic**: ``UDR``
- **Partitioning Strategy**: Load-balanced
- **Message Encoding**: JSON (UTF-8)
- **Transport Security**: TLS (TLS 1.2+ supported)

Partitioning Behavior
---------------------

Partition selection is managed automatically by the Kafka writer using a load-balancing strategy (``LeastBytes`` balancer).

The message key is set to:

    ``<topic>-<partition-config-value>``

However, the partition is not explicitly enforced; the balancer determines the final partition assignment.

Security Configuration
----------------------

If enabled, Kafka connections use TLS with:

- Minimum TLS version: 1.2
- Configurable certificate verification
- 10-second dial timeout
- Dual-stack (IPv4/IPv6) support

Authentication and additional security parameters depend on the deployment environment.

Reporting Frequency
-------------------

Usage data must be reported periodically.

The recommended reporting interval is:

    **900 seconds (15 minutes)**

Each reporting cycle should:

- Measure all active resources.
- Publish one usage record per resource.

Billing Granularity and Accuracy
--------------------------------

Billing precision is directly proportional to reporting frequency.

Example:

If a resource scales from size ``1`` to ``100``, the billing system recognizes the change at the timestamp provided in the first usage record reporting size ``100``.

If reporting intervals are too long:

- Scaling events may be recorded later than their actual occurrence.
- Short-lived scale-up/scale-down events within a single interval may not be captured.
- Billing accuracy may decrease.

To maintain accurate billing:

- Use sufficiently short reporting intervals.
- Ensure timestamps reflect actual measurement time.
- Avoid producing duplicate usage records.

Operational Considerations
--------------------------

- Producers run concurrently and may send multiple messages in parallel.
- Ordering is preserved per partition only.
- Message validation (JSON marshaling) must succeed before publishing.
- Errors during transmission should be logged and monitored.

Failure to comply with these requirements may result in inaccurate billing calculations.