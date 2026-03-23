# FlexRIC O-RAN Security Evaluation

## Project Overview
This repository presents a scoped security evaluation of FlexRIC in the Open RAN (O-RAN) / Near-RT RIC context. Based on a bachelor thesis, it translates the analysis of xApp-related attack surfaces in a complex distributed platform into concrete hardening recommendations.

*For repository boundaries and scope limitations, see [`docs/repository-scope.md`](docs/repository-scope.md).*

## System Context
FlexRIC implements a Near-RT RIC architecture in which third-party extensibility (xApps) interacts with controller logic and RAN-facing interfaces. This architecture makes the trust boundary between xApps and controller-side logic critical for service integrity and stability.

- **Platform:** FlexRIC / Near-RT RIC  
- **Environment:** Linux, C, E2 node emulation  
- **Communication:** SCTP-based  

## What Was Evaluated
The evaluation focused on architecture, interfaces, and xApp-related attack surfaces in FlexRIC, including:

- System trust boundaries and interface analysis  
- Evaluation of known attack patterns against FlexRIC  
- Design of **two original attack scenarios**  
- Review of permission handling, subscription ownership validation, message validation, and resource-exhaustion-related behavior  

## Main Findings
The evaluation identified several important weaknesses in how FlexRIC handled untrusted xApp behavior:

- **Permission handling:** insufficient control over access to critical functions  
- **Subscription ownership validation:** weak ownership checks enabled potential cross-xApp interference  
- **Message validation:** insufficient validation of incoming messages and request context  
- **Resource behavior:** architectural conditions that could contribute to resource exhaustion  

A key takeaway was that even authenticated xApps should be treated as untrusted actors and validated accordingly.

## Recommendations
The project translated the findings into practical hardening recommendations, including:

- Stronger access control / RBAC for xApp actions  
- Ownership and context validation for subscription-related operations  
- Stricter validation of incoming requests and parameters  
- Rate limiting for high-volume or abusive behavior  
- Runtime resource monitoring and containment  

## Limitations
This was a scoped academic evaluation conducted in an emulated environment. The findings apply to the tested FlexRIC setup and should not be presented as claims about commercial production deployments or all Near-RT RIC implementations.

This repository does **not** include thesis source code, exploit scripts, weaponized material, step-by-step attack instructions, or production-ready remediation claims.

## Why This Project Matters
This case study demonstrates capabilities relevant to Technical Consulting, Cyber, and Solution-oriented roles:

- Understanding of a complex distributed technical system  
- Architecture-level security reasoning rather than isolated bug discussion  
- Structured analysis of trust boundaries and control weaknesses  
- Translation of technical findings into practical hardening recommendations  

Together with a separate local RAG MVP repository, this project helps show both sides of my profile: bounded enterprise AI solution thinking and disciplined analysis of complex technical systems and security architecture.
