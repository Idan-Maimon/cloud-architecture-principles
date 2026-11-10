# Cross-Cutting Principles

Principles that apply to every quality goal. Principles 1–5 follow the Google Cloud Architecture Framework core principles; principle 6 follows the ISO/IEC 25010 guidance for the AI era.

1. **Design for change.** Ship small, frequent changes and get fast feedback.
2. **Document your architecture.** Every service maintains architecture documentation and ADRs, using arc42.
3. **Simplify.** Start minimal and use platform services before building your own.
4. **Decouple.** Components are upgraded, secured, scaled and monitored independently.
5. **Prefer stateless.** Keep state in managed data services, not in compute.
6. **Verify every change against every quality.** AI-generated and human-written code pass the same automated quality gates (security, maintainability, reliability) before release. Generation is no longer the bottleneck; verification is.
