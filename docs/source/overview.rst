================
Overview
================

Introduction
#############

This documentation describes a pricing and resource accounting system built around
well-defined SKUs, measurable metrics, structured ingestion pipelines, subscription
plans, and pricing rules.

The system is designed to:

- Standardize how resources are defined and measured
- Collect usage data in a reliable and scalable way
- Apply pricing logic consistently
- Enable flexible subscription plan configuration
- Support both testing and production-grade deployments


Core Concepts
#############

SKU (Stock Keeping Unit)
=========================

An SKU represents a billable resource type. Every measurable resource must first be
defined as an SKU before it can be reported, aggregated, or priced.

Examples:

- Server
- Disk
- Network traffic
- API request

Metrics model
==============

Metrics define *how* an SKU is measured.

Examples:

- Count
- Storage in GB
- Duration in hours
- Data transferred in MB

Metrics ensure that usage is quantifiable and comparable across systems.


Sending Data
=============

Ingestion is the process of collecting usage data from collectors or external systems
and transforming it into structured, billable records.

The ingestion pipeline is responsible for:

- Validating incoming data
- Associating usage with defined SKUs
- Storing usage events
- Preparing data for aggregation and billing

It supports both testing environments and production workloads.


Plan
=====

Plans define subscription-level rules and limits.

A plan may:

- Restrict access to certain SKUs
- Define quotas
- Apply discounts
- Enable feature-based billing models

Plans allow differentiated offerings (e.g., Free, Standard, Enterprise).


Pricing
========

Pricing rules determine how usage is converted into monetary cost.

Pricing can include:

- Fixed prices
- Usage-based pricing
- Tiered pricing
- Discounts
- Promotions

The pricing engine applies these rules to aggregated usage data to compute final charges.


System Flow
#############

1. SKUs are defined.
2. Metrics describe how they are measured.
3. Usage data is ingested.
4. Plans determine eligibility and limits.
5. SKU pricing defines resource cost.
6. Final charges are generated.
