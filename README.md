```mermaid
graph TD
    UI[Terminal App UI] -->|1. POST /api/payments/| API[api/terminal_gateway]
    API -->|2. Route Validated Request| Processor[lib/payment_processor]
    Processor -->|3. /purchase| Terminal[Payment Terminal]
    Processor -.->|4. Return AWAITING_CARD| UI
    Terminal -.->|5. Customer Taps Card| Terminal
    UI -->|6. GET /status Polling| Processor
    Processor -->|7. Payment Success / Sales Order| Upstream[lib/upstream_integration]
    Upstream -->|8. POST /authorize-payment & /apply-payment| Bank[Upstream Acquiring Gateway]
