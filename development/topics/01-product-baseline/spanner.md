---
id: spanner
type: topic
title: "Spanner"
description: "Spanner Product Playbook"
status: published
difficulty: beginner
duration: 10 min
topics: [gcp]
product_id: spanner
learning_mode: lab
lab_modes: [codelab]
default_lab_mode: codelab
tags: [spanner]
collections: [col-google-cloud]
---
{{< step label="Spanner Product Playbook" duration="9:00" >}}

# Spanner

> **Product Baseline — standalone product knowledge block.**
> This file contains the product knowledge needed to study this product independently.

## Learning Map

By the end of this chapter, you should be able to reason about:

- Distributed relational model
- Strong consistency and transactions
- Horizontal scale and schema/key design
- Regional vs multi-region configurations
- Availability and RPO/RTO implications
- Query/access-pattern design
- Spanner vs Cloud SQL/AlloyDB/Bigtable

## Official Learning Resources

- [Official documentation](https://docs.cloud.google.com/spanner/docs)
- [Quickstart / get started](https://docs.cloud.google.com/spanner/docs/create-query-database-console)

{{< /step >}}

{{< step label="Product Identity" duration="9:00" >}}

## Product Identity

- **Plain-language purpose:** Scalable, always-on, multi-model DB.

- **Catalogue category:** Databases
- **Catalogue summary:** Scalable, always-on, multi-model DB
- **Known aliases:** Spanner, Cloud Spanner
### Need to Know

**Spanner --- horizontally scalable relational database with strong
consistency.** It belongs to operational relational serving, not
warehouse analytics.

### When to Choose

Choose Spanner when the workload genuinely needs relational semantics
plus horizontal/global scale and strong consistency.

### Common Patterns

| Pattern | Product guidance |
| --- | --- |
| Globally distributed relational data | Use Spanner when relational transactions must operate at horizontal or global scale. |
| Strong consistency with scale | Choose Spanner when strong transactional consistency is required together with distributed scale. |
| Conventional relational workload | Prefer a conventional managed relational database when its scale and availability model already satisfies the workload. |
| Analytical warehouse workload | Prefer BigQuery when the dominant requirement is analytical scanning and aggregation rather than transactional serving. |

### Common Anti-Patterns

-   Choosing Spanner simply because a workload uses SQL.
-   Using it for analytical warehouse scans better suited to BigQuery.
-   Modernizing a conventional database to Spanner when Cloud SQL
    satisfies the stated scale/availability needs.

### Open Source / Existing Platform → Google Product

Traditional relational → **Spanner** is usually an architectural
modernization. Expect schema/key/application considerations rather than
a zero-change migration.

### Architecture

``` mermaid
flowchart TD
    A[Relational workload] --> B{Conventional scale?}
    B -->|Yes| C[Cloud SQL]
    B -->|No| D{Need horizontal/global scale + strong consistency?}
    D -->|Yes| E[Spanner]
    D -->|No, analytics| F[BigQuery]
```

### Adjacent Products / Decision Boundaries

**Spanner --- global/horizontal relational** \| **Cloud SQL ---
conventional relational** \| **BigQuery --- analytical SQL**.

### Performance, Reliability, Security & Cost

Evaluate transaction semantics, key design, locality, availability and
operational scale. The distinctive product boundary is the combination of **relational +
scale/consistency**, not SQL alone.

{{< /step >}}

{{< step label="Terminology for Reasoning" duration="9:00" >}}

## Terminology for Reasoning

Start with the product's own vocabulary. The third column turns each term into a reasoning cue rather than a definition to memorize.

| Product term | Meaning | Why it matters when reasoning |
| --- | --- | --- |
| **Instance** | Compute and regional/multi-region deployment resource that hosts databases. | Topology and capacity decisions start here, while schemas and transactions live in databases. |
| **Database** | Relational schema and data container within a Spanner instance. | Transactional and schema design decisions are scoped to the database. |
| **Split** | Range of keyspace that Spanner independently distributes and serves. | Primary-key design influences split distribution, locality, and hotspot risk. |
| **Primary key** | Ordered key defining row identity and physical key order. | Monotonically increasing leading keys can concentrate writes; key design is a scaling decision. |
| **Interleaved table** | Child table whose rows can be colocated by key hierarchy with parent data. | Useful when hierarchical locality matters; not a generic normalization mechanism. |
| **Read-write transaction** | Transaction providing serializable read/write semantics. | Choose when operations must atomically read and modify data. |
| **Read-only transaction** | Consistent read across one or more reads at a timestamp. | Useful for consistent multi-read workloads without write locks. |
| **Change stream** | Ordered change records emitted from selected Spanner data. | Signals downstream CDC/event processing rather than polling the transactional tables. |

### Cross-product reasoning vocabulary

| Reasoning term | Meaning |
| --- | --- |
| **Purpose** | The primary problem the product exists to solve. |
| **Workload shape** | The characteristic form of the work, such as batch, streaming, transactional, analytical, orchestration, messaging, or storage. |
| **Architectural layer** | Where the product acts in the system, such as ingestion, transport, processing, storage, serving, orchestration, governance, security, or operations. |
| **Operational model** | What Google manages and what the customer still configures, secures, monitors, and operates. |
| **Decision boundary** | The requirement that makes this product a better or worse fit than an adjacent product. |
| **Anti-pattern** | A requirement or design choice that conflicts with the product's purpose or operating model. |

Use the product terms first, then use the cross-product vocabulary to explain why those concepts change an architectural decision.

{{< /step >}}

{{< step label="Knowledge Check" duration="9:00" >}}

## Knowledge Check

| Question | Resolution guidance |
| --- | --- |
| What primary workload is Spanner designed to solve? | **Resolve:** Spanner is primarily for **scalable, always-on, multi-model db**. Then classify that purpose by workload shape and architectural layer, and explain why that makes the service a fit. Do not stop at a feature list. |
| When is Spanner the wrong choice? | Use the anti-patterns and decision boundaries. Name cases where another product better matches the workload, access pattern, compatibility, failure domain, or operational-control requirement. |
| What adjacent products are most easily confused with it? | State the decisive boundary as: **Choose X when …; choose Y when …**. Prefer workload and constraint reasoning over feature lists. |
| What operational responsibilities remain with the customer? | Separate what Google manages from what the customer must still design, configure, secure, monitor, test, or operate. |
| What reliability, security, performance, and cost factors matter most? | Explain the important failure boundaries, controls, performance levers, and cost drivers, including why each design choice changes the outcome. |
| How would you recognize Spanner without seeing the product name? | Recognize the workload, hard constraints, architectural layer, compatibility requirements, and operational model—the **problem signature** that points toward Spanner. |

{{< /step >}}

{{< step label="Conclusion" duration="1:00" >}}

## Conclusion

- **Start with the workload:** understand the problem Spanner is designed to solve before memorizing features.
- **Use constraints to decide:** access pattern, compatibility, failure domain, operational ownership, security, performance, and cost should drive the choice.
- **Know the boundaries:** explain when an adjacent product is a better fit and why.
- **Reason about operations:** distinguish managed capabilities from customer responsibilities.
- **Recognize the problem signature:** identify Spanner from architectural requirements even when its name is absent.
- **Revisit weak areas:** use the Learning Map and Knowledge Check to decide what to review next.

{{< /step >}}

{{< step label="Maintenance Notes" duration="1:00" >}}

## Maintenance Notes

Prefer durable product facts and product-level decision boundaries. Verify volatile runtime, version, quota, pricing, and availability details against official product documentation before updating this material.

{{< /step >}}
