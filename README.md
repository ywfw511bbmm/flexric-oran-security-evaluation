# FlexRIC O-RAN Security Evaluation

[Case Study](docs/thesis-case-study.md) · [Repository Scope](docs/repository-scope.md)

## 1. Project Overview
This repository presents a scoped security evaluation of FlexRIC in the Open RAN (O-RAN) / Near-RT RIC context. The project focused on xApp-related attack surfaces in a complex distributed platform and translated the findings into concrete hardening recommendations.

This repository is documentation-first. It is intended to show system context understanding, architecture analysis, security evaluation, and practical hardening thinking. It does not include thesis code or exploit-style reproduction material.

## 2. System Context
FlexRIC is an implementation of a Near-RT RIC architecture in which third-party xApps can interact with controller logic and RAN-facing interfaces. This creates a useful but security-sensitive platform: extensibility is valuable, but the trust boundary between xApps and controller-side logic becomes critical.

Evaluation context:
- Platform: FlexRIC / Near-RT RIC
- Environment: Linux, C, E2 node emulation
- Communication: SCTP-based communication

## 3. Security Problem
When a distributed control platform allows third-party xApps to interact with controller behavior, weak validation or insufficient access control can affect service integrity, operational stability, and platform trust. The core question in this thesis was whether known xApp-related risks also apply to FlexRIC and what FlexRIC-specific weaknesses emerge from its architecture.

## 4. What Was Evaluated
This thesis focused on architecture, interfaces, and xApp-related attack surfaces in FlexRIC. The work included:
- analysis of the underlying system context and interface boundaries
- evaluation of known attack patterns against FlexRIC
- design of two original attack scenarios
- review of permission handling, subscription ownership validation, message validation, and resource-exhaustion-related behavior

## 5. Main Findings
The evaluation identified several important weaknesses in how FlexRIC handled untrusted xApp behavior:
- **Permission handling:** insufficient control over access to critical functions
- **Subscription ownership validation:** weak ownership checks enabled potential cross-xApp interference
- **Message validation:** insufficient validation of incoming messages and request context
- **Resource behavior:** architectural conditions that could contribute to resource exhaustion

A key takeaway was that even authenticated xApps should be treated as untrusted actors and validated accordingly.

## 6. Recommendations
The project proposed concrete hardening recommendations, including:
- stronger access control / RBAC for xApp actions
- ownership and context validation for subscription-related operations
- stricter validation of incoming requests and parameters
- rate limiting for high-volume or abusive behavior
- runtime resource monitoring and containment

## 7. What This Repository Does Not Include
This repository does not include:
- thesis source code
- step-by-step exploit instructions
- weaponized offensive material
- production-ready patches
- enterprise deployment or client delivery claims

For repository boundaries, see `docs/repository-scope.md`.

## 8. Limitations
This was a scoped academic evaluation conducted in an emulated environment. The findings are tied to the tested FlexRIC setup and should not be presented as claims about commercial production deployments or all Near-RT RIC implementations.

## 9. Why This Project Matters for Technical Consulting / Cyber / Solution Roles
This project demonstrates:
- the ability to understand a complex distributed technical system
- architecture-level security reasoning rather than isolated bug discussion
- structured evaluation of trust boundaries and control weaknesses
- practical hardening recommendations with clear scope and limitations

Together with my separate RAG MVP repository, this project helps show both sides of my profile: scoped solution thinking for enterprise AI use cases, and disciplined analysis of complex technical systems and security architecture.
