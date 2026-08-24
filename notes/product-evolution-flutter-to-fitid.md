# Chanamill Product Evolution: Flutter Prototype to FitID System

Chanamill did not begin as a narrowly isolated fit engine. Early product work explored the broader commerce surface first, which exposed which parts of the system were generic commerce and which part represented a differentiated technical problem.

## Early mobile prototype

The Flutter prototype explored:

- home/discovery navigation
- stories and short-form product content
- product/catalog models
- variants, cart, order and payment domain objects
- creator/store concepts
- configurable/personalized product flows
- image upload and scanning experiments
- mobile-first state management

That work was useful because it established the end-to-end commerce shell.

## Web product evolution

The web product then narrowed the experience around apparel personalization:

- measurement onboarding
- FitID creation
- explainable shirt/pant recommendations
- configurable and made-to-measure ordering
- garment visualization
- Designer Store concepts
- AI/personal-stylist flows

## Why the architecture narrowed around FitID

The commerce primitives were solvable with conventional product architecture. The harder problem was persistent apparel fit state.

```text
Generic commerce
product → cart → order

Differentiated loop
measurement → FitID → garment spec → fit decision
           → manufactured/delivered outcome → better FitID
```

This changed the architectural center of gravity. Instead of treating personalization as UI state attached to a product page, FitID becomes a versioned domain object used by recommendation, visualization, ordering, manufacturing and feedback.

## 3D and capture work

Later 3D/avatar and garment-mesh work adds another consumer of the same versioned domain state. It should not fork fit logic into rendering code. The renderer receives FitID/spec versions and presentation assets, while measurement confidence and fit decisions remain owned by the personalization domain.

## Design lesson

Prototype breadth can be valuable when it reveals the true system boundary. In this case, building discovery, social, cart, customization and order flows made it clearer that the defensible engineering problem was not another storefront—it was connecting physical body data, garment construction, production and delivered outcomes through a persistent fit identity.