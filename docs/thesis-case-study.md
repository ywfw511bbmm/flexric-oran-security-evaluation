# Thesis Case Study: FlexRIC Security Evaluation

## System Context
Open RAN introduces more open and programmable control architectures into the radio access network domain. In the Near-RT RIC model, third-party xApps can observe network state and influence controller behavior. This improves flexibility, but it also makes interface boundaries, validation logic, and trust assumptions more important.

This thesis focused on FlexRIC, using a Linux/C-based setup with E2 node emulation and SCTP-based communication.

## Security Problem
The main security question was not just whether individual bugs existed, but whether FlexRIC’s architecture and control model exposed xApp-related weaknesses that could affect system integrity or availability. The work therefore focused on how untrusted or insufficiently constrained xApps interact with controller-side logic and shared platform resources.

## Evaluation Scope
The evaluation covered:
- architecture and interface analysis
- xApp-related attack surface analysis
- evaluation of known attack patterns in the FlexRIC context
- design of two original attack scenarios
- review of permission handling, ownership validation, message validation, and resource-exhaustion-related behavior

## Main Findings
The thesis identified four main areas of weakness:
1. **Permission handling:** insufficient control over sensitive xApp actions
2. **Subscription ownership validation:** missing or weak ownership checks for subscription-related operations
3. **Message validation:** insufficient validation of request structure, context, or source assumptions
4. **Resource behavior:** architectural conditions that could contribute to resource exhaustion under abusive or poorly constrained xApp behavior

These findings reinforced the need to treat authenticated xApps as untrusted by default unless explicit control and validation mechanisms are in place.

## Recommendations
Based on the findings, the thesis proposed practical hardening measures:
- **Stronger access control:** introduce stricter access control / RBAC for xApp actions
- **Ownership and context validation:** validate subscription ownership and request context before allowing sensitive operations
- **Message and parameter validation:** strengthen validation for incoming requests and reporting-related parameters
- **Rate limiting:** reduce the impact of abusive or excessive request behavior
- **Runtime monitoring and containment:** monitor CPU / memory behavior and contain harmful xApp activity when needed

## Limitations
This was a scoped academic security evaluation, not a production hardening project. It was conducted in an emulated environment and should not be framed as a claim about live commercial deployments. The findings are specific to the tested FlexRIC context.

## Why It Matters
This case study shows the ability to analyze a complex distributed platform, reason about trust boundaries and controller behavior, and convert technical findings into clear, practical hardening recommendations. For recruiter and hiring-manager review, the most relevant signal is disciplined architecture and security thinking with clear scope control.
