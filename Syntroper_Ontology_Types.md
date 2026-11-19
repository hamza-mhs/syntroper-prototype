# Syntroper ontology · types (draft for dev review)

Draft written for Hassan to react to. It follows Arsalan's rule: **an integration point is an endpoint or resource, not a method.** The way something reaches that point (HTTP GET, POST, an event, and so on) is the **integration type**, recorded on each integration.

## Element kinds

| Kind | What it is | Example |
|---|---|---|
| Channel | An app a person uses to reach the system | Storefront (Next.js), Admin dashboard |
| Persona | Who a use case is for | Shopper, Store admin, Finance |
| Use case | A goal a persona gets done, made of steps | Cancel an order |
| Step | One user action and the system's response | "Confirm in the dialog" → "Cancels it, releases stock" |
| API operation | One method on one route | `POST /admin/orders/:id/cancel` |
| Bounded context | A group of logic that owns its data | Orders, Payments |
| Integration point | A resource one context exposes or calls (see point types) | `/admin/reservations` |
| Integration | One connection from a caller to an integration point, with one integration type | Orders → `/admin/reservations` · HTTP DELETE |
| Outside system | Something we call but can't see inside | Payment provider |
| Runtime provider | What runs the code | Node.js server, Redis, Postgres |
| Software system | A whole system as one box | Commerce platform |

## Integration point types (what the point is)

| Type | Identity of the point | Accepts these integration types |
|---|---|---|
| HTTP resource | Route path up to the resource, without the method: `/admin/reservations`, `/store/carts/:id/line-items` | HTTP GET, POST, PUT, PATCH, DELETE |
| gRPC service | Service name: `shipping.Rates` | gRPC call (unary, stream) |
| Event topic | Event name: `order.placed` | Event publish, Event subscribe |
| Module interface | In-process service or workflow entry: `createPaymentSessionsWorkflow` | Module call, Workflow step |
| Data link | Link between two modules' data: `order ↔ customer` | Module link |
| Data store | Table, collection or key pattern: `reservation_item`, `cart:{id}` | SQL read, SQL write, Cache read/write, Lock |
| External endpoint | Address outside the scanned code: `PAYMENT_SERVICE_ADDR` | Outbound HTTP, Outbound gRPC, Webhook in |

## Integration types (how the call is made)

| Group | Types |
|---|---|
| HTTP | HTTP GET, HTTP POST, HTTP PUT, HTTP PATCH, HTTP DELETE |
| RPC | gRPC call (unary), gRPC stream |
| Events | Event publish, Event subscribe |
| In-process | Module call, Workflow step, Module link |
| Data | SQL read, SQL write, Cache read, Cache write, Lock |
| Outside | Outbound HTTP, Outbound gRPC, Webhook in |

## Rules

1. Each REST route with several methods is **one** integration point with several integration types. `GET`, `POST` and `DELETE` on `/admin/reservations` are three integrations at one point, not three points.
2. Each integration has exactly one integration type, one caller and one integration point.
3. An integration point lists the integration types it accepts. The UI shows counts per type: "POST ×1 · DELETE ×1".
4. Direction comes from the integration (caller → point), not from the point.

## Other types already in the product

| Type set | Values |
|---|---|
| Health | Live, Degraded, Down, Not scanned |
| Review status (use cases) | To review, Changes requested, Accepted, Rejected (hidden) |
| Trust (elements found by Syntroper) | Code evidence, Derived from source, Suggested, Needs clarification, Confirmed |
| Alternate flow kinds | Error, Validation, Cancel |
| Dependency decision (when moving logic) | Call it there, Move it, Copy it, Turn into an event, Ignore |

Open question for dev: should Data store points be their own Galaxy layer, or stay inside integration points?
