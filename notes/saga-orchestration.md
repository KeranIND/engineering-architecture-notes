# Saga Orchestration vs Choreography

A multi-step business workflow often crosses services that cannot share one database transaction. Sagas model the workflow as local transactions plus compensating actions.

## Orchestration

A coordinator owns the workflow state and issues the next command explicitly.

Advantages:
- state transitions are visible
- easier to reason about compensation
- simpler operational debugging
- business workflow is discoverable in one place

Costs:
- coordinator can become overly central
- requires disciplined service boundaries

## Choreography

Services react to events and publish new events without a central coordinator.

Advantages:
- loose coupling
- natural fit for simple event reactions

Costs:
- control flow becomes implicit
- cyclic event chains are easy to create
- difficult to answer "what happens next?"
- compensation logic can become distributed across many services

## Rule of thumb

Use choreography for independent reactions to facts. Prefer explicit orchestration when a workflow has a defined beginning/end, ordered steps, compensation, and business-critical state.
