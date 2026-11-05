---
name: order-status
description: Explain a fictional Northstar order status using the sample Orders API contract when a user asks about an order.
metadata:
  version: "1.0.0"
  sample: "true"
---

# Order status

## Inputs

An order identifier, such as `ORD-1001`, and an order response provided by the user or a configured tool.

## Procedure

1. Ask for an order identifier if none is supplied.
2. Use the contract in `../../rest/orders/openapi.yaml` to interpret the response.
3. Explain the status, total, and currency without inventing delivery dates.
4. If no response is available, use the contract's example only and explicitly label the answer as simulated.
5. If the response is not found, report that outcome rather than fabricating an order.

## Example

For the contract's `ORD-1001` fixture: “Simulated result: order ORD-1001 is shipped; its total is EUR 49.95.”

## Limitations

The API endpoint is fictional. Do not call it, request payment credentials, or claim to have retrieved live customer data.
