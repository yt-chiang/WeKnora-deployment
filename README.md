
This deployment keeps the same [WeKnora](https://github.com/Tencent/WeKnora) architecture, but intentionally changes compose behavior for an isolated environment.

- Adds a dedicated DNS layer (CoreDNS) and split network design (`internet` + internal network) to make outbound resolution and egress routing controllable and predictable.
- Moves host exposure behind an Nginx reverse proxy, so frontend/app traffic is centralized at one edge point instead of exposing app containers directly.
- Introduces a Squid sidecar to support policy-based outbound control (auditability, filtering, and easier corporate-network compliance).
- Pins several services to use the internal DNS policy (`dns: 10.218.20.53`) for consistent name resolution across containers.