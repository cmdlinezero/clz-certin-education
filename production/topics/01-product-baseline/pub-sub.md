---
id: pub-sub
type: topic
title: "Pub/Sub"
description: "Pub/Sub Product Playbook"
status: published
difficulty: beginner
duration: 10 min
topics: [gcp]
product_id: pub-sub
learning_mode: lab
lab_modes: [codelab]
default_lab_mode: codelab
tags: [pub-sub]
collections: [col-google-cloud]
---
{{< step label="Pub/Sub Product Playbook" duration="9:00" >}}

# Pub/Sub

> **Product Baseline — standalone product knowledge block.**
> This file contains the product knowledge needed to study this product independently.

## Learning Map

By the end of this chapter, you should be able to reason about:

- Topics, subscriptions, publishers and subscribers
- Push vs pull delivery
- At-least-once delivery, acknowledgement and redelivery
- Ordering, replay/retention and dead-letter handling
- Fan-out and independent consumer semantics
- Throughput, backpressure and subscriber scaling
- Security and private connectivity
- Pub/Sub vs Kafka-compatible messaging

## Official Learning Resources

- [Official documentation](https://docs.cloud.google.com/pubsub/docs)
- [Quickstart / get started](https://docs.cloud.google.com/pubsub/docs/publish-receive-messages-client-library)

{{< /step >}}

{{< step label="Product Identity" duration="9:00" >}}

## Product Identity

- **Plain-language purpose:** Global real-time messaging.

- **Catalogue category:** Analytics
- **Catalogue summary:** Global real-time messaging
- **Known aliases:** Pub/Sub, Cloud Pub/Sub
### Need to Know

**Pub/Sub --- managed asynchronous event ingestion and delivery.** A
topic represents the published stream; a subscription owns independent
delivery state for a consumer workload.

### When to Choose

Choose Pub/Sub when producers and consumers need to be decoupled, events
arrive continuously, or multiple independent consumers need the same
event stream.

### Common Patterns

| Pattern | Product guidance |
| --- | --- |
| Event ingestion and buffering | Use Pub/Sub to accept and buffer asynchronous events between producers and consumers. |
| Decoupled consumers | Give independent logical consumers separate subscriptions when each consumer must receive every event. |
| Shared worker pool | Multiple workers processing one logical workload can consume from the same subscription. |
| Streaming pipeline chain | A common architecture is Pub/Sub for transport, Dataflow for transformation, and BigQuery for analytical storage. |
| Incompatible consumer rollout | Use an independent subscription for a new incompatible consumer or pipeline so old and new versions do not compete for the same delivery state. |

> **Boundary:** Pub/Sub transports and buffers events; it is not the transformation engine or analytical database.

{{< /step >}}

{{< step label="Terminology for Reasoning" duration="9:00" >}}

## Terminology for Reasoning

Start with the product's own vocabulary. The third column turns each term into a reasoning cue rather than a definition to memorize.

| Product term | Meaning | Why it matters when reasoning |
| --- | --- | --- |
| **Topic** | Named resource to which publishers send messages. | Represents the producer-facing event channel; consumers do not normally compete directly on the topic. |
| **Subscription** | Named delivery resource attached to a topic. | Each subscription has independent delivery state, so separate logical consumers usually need separate subscriptions. |
| **Publisher** | Producer that sends messages to a topic. | Publisher independence is part of Pub/Sub's asynchronous decoupling model. |
| **Subscriber** | Consumer that receives messages through a subscription. | Scale and delivery behavior are reasoned about at the subscription/subscriber side. |
| **Acknowledgment** | Subscriber signal that processing of a delivered message succeeded. | Failure to acknowledge can cause redelivery; processing must account for delivery semantics. |
| **Ack deadline** | Time allowed before an unacknowledged message becomes eligible for redelivery. | Too-short deadlines can create avoidable redelivery; extending them is not a substitute for healthy consumers. |
| **Dead-letter topic** | Topic used for messages that cannot be processed successfully after configured delivery attempts. | Provides an isolation/recovery path for poison messages rather than infinite normal-path retries. |
| **Ordering key** | Message attribute used to request ordered delivery for related messages. | Choose ordering only where per-key order is a real requirement because it constrains delivery behavior. |

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
| What primary workload is Pub/Sub designed to solve? | **Resolve:** Pub/Sub is primarily for **global real-time messaging**. Then classify that purpose by workload shape and architectural layer, and explain why that makes the service a fit. Do not stop at a feature list. |
| When is Pub/Sub the wrong choice? | Use the anti-patterns and decision boundaries. Name cases where another product better matches the workload, access pattern, compatibility, failure domain, or operational-control requirement. |
| What adjacent products are most easily confused with it? | State the decisive boundary as: **Choose X when …; choose Y when …**. Prefer workload and constraint reasoning over feature lists. |
| What operational responsibilities remain with the customer? | Separate what Google manages from what the customer must still design, configure, secure, monitor, test, or operate. |
| What reliability, security, performance, and cost factors matter most? | Explain the important failure boundaries, controls, performance levers, and cost drivers, including why each design choice changes the outcome. |
| How would you recognize Pub/Sub without seeing the product name? | Recognize the workload, hard constraints, architectural layer, compatibility requirements, and operational model—the **problem signature** that points toward Pub/Sub. |

{{< /step >}}

{{< step label="Conclusion" duration="1:00" >}}

## Conclusion

- **Start with the workload:** understand the problem Pub/Sub is designed to solve before memorizing features.
- **Use constraints to decide:** access pattern, compatibility, failure domain, operational ownership, security, performance, and cost should drive the choice.
- **Know the boundaries:** explain when an adjacent product is a better fit and why.
- **Reason about operations:** distinguish managed capabilities from customer responsibilities.
- **Recognize the problem signature:** identify Pub/Sub from architectural requirements even when its name is absent.
- **Revisit weak areas:** use the Learning Map and Knowledge Check to decide what to review next.

{{< /step >}}

{{< step label="Maintenance Notes" duration="1:00" >}}

## Maintenance Notes

Prefer durable product facts and product-level decision boundaries. Verify volatile runtime, version, quota, pricing, and availability details against official product documentation before updating this material.

{{< /step >}}
