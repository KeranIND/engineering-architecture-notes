# Creator Commerce as an Attribution Layer

Chanamill's creator-commerce model should sit on top of the same FitID, product, order and manufacturing systems rather than fork them into a separate marketplace architecture.

## Flow

```text
Creator storefront
      ↓
Product / style discovery
      ↓
FitID-aware product decision
      ↓
Order
  + creator attribution
      ↓
Production / fulfillment
      ↓
Commission settlement
      ↓
Delivered-fit feedback
```

## Design rules

- creator attribution belongs to the order snapshot
- product and garment-spec identity stay canonical
- commission policy is versioned independently from the order
- creator storefronts do not own FitID
- fit feedback returns to the customer/product loop, not only creator analytics
- fulfillment and manufacturing remain shared platform capabilities

The architectural benefit is that creator distribution becomes another acquisition and merchandising surface without fragmenting the core identity and fulfillment systems.