# TD.Next Usability and Design Work Items

Changes that improve readability, the usability of the specification OR development, spec generation, bug fixes, and testing of the specification do not need use cases.
These have more priority since they can impact how new features look like in a TD instance.

## Design Document

We should start a TD (re)design document that explains the idea behind the design of different features. See [issue 1889](https://github.com/w3c/wot-thing-description/issues/1889).

## Document reorganization

Changes that should be done while keeping the current content

### Common Definition Section

Usability and readability improvements for not needing to "jump around" while reading

### Grouping of Normative Requirements

Making sure that important normative text is not scattered around too much.

### Assertion id Alignment

Adding `td`, checking naming scheme

### Better Integration of Thing Model

There were questions about how much a TM is related to the TD.
Some discussion might be needed.

## Synchronization with Other Documents

### Discovery Sync

Moving discovery-related text from TD to Discovery

### Architecture Sync

Checking overlaps with architecture.

## Reusable TD Elements

### Reusable Connections

Currently, each form of an affordance has information on the endpoint, media type and other protocol related information. 
It is possible to use the base term for simplifying the endpoint but it has limitations such as:

- If the media type is also common across forms, it is repeated
- Multiple bases are not possible
- For protocols that are based on an initial connection and then subsequent messages, the semantics are not clear.

Thus, a mechanism to describe connection and protocol information that can be used by other forms is needed. 
In protocols with initial connection, this can be also used to indicate what needs to be done by the Consumer before executing any operation.

Related Issues:

- <https://github.com/w3c/wot-thing-description/issues/1664>
- <https://github.com/w3c/wot-thing-description/issues/1248>
- <https://github.com/w3c/wot-thing-description/issues/1242>
- <https://github.com/w3c/wot-thing-description/issues/878>

### Data Schema Mapping

Also known as: Mapping TD elements to messages

How can we represent all protocol messages sent and received?
It should be using data schema to indicate application-specific parameters but we should be able to describe payload, header, uri variables, and other protocol parameters.

Related Issues:

- BACnet URI Variables discussion

### Security Schemes Refactoring

The need to be refactored and use the same pattern as other reusable elements

### Inline Security

Simplifying the way to describe security when there is only one mechanism needed to be described (in contrast to needing two terms at the moment)

Relevant discussions:

- https://github.com/w3c/wot-thing-description/pull/945

### Reusable Element Design

Scenarios, requirements, and use the same pattern for all reusable elements.
This will influence the items above.

Related discussions:

- https://github.com/w3c/wot-thing-description/pull/1341 (but many are linked here as well)

## Affordance Uniformity

Uniform pattern/state machines between Actions, Events, and Properties.

- Avoid doing the same thing in a different way, for example how to express observability and cancellation
- Relationships across affordances, for example when an Action changes the state of a Property
- Property vs. Action (also URI Variables redesign question)

## Normative Parsing, Validation, Consumption

Currently, the TD specification defines an abstract information model and a default JSON serialization for TDs.
However, parsing, consuming and validating TDs are not normatively defined.
A validation process is defined but is not normative, which leads to certain ambiguities for a Consumer parsing a TD.
Additionally, no method is proposed for validation of the extensions that are used via the prefixes and the @context.
The WG will specify normative algorithms for parsing, consuming and validating TDs to ensure interoperability of Consumers.

### TD Validation

What is a valid TD, are there any levels of validness?

- A TD validator can do only JSON Schema validation but that is not enough to test everything.
- A TD may be not completely valid but usable by a "degraded consumer" (see below) or a TD can be completely valid according to all the assertions and protocol bindings but not be usable by some consumers.

Additionally, we need better validation of protocols and associated security in the TD.

### Consumption Rules

Do we want to prescribe how TDs are processed and consumed beyond the text level?

### Degraded Consumption

- Rule for uniform degradation across consumers, e.g. TD too big, protocol or protocol options unknown, contentType unknown, etc.
