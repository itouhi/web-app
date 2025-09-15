# Feature Specification: [FEATURE NAME]

**Feature Branch**: `[###-feature-name]`  
**Created**: [DATE]  
**Status**: Draft  
**Input**: User description: "$ARGUMENTS"

## Execution Flow (main)
```
1. Parse user description from Input
   → If empty: ERROR "No feature description provided"
2. Extract key concepts from description
   → Identify: actors, actions, data, constraints
3. For each unclear aspect:
   → Mark with [NEEDS CLARIFICATION: specific question]
4. Fill User Scenarios & Testing section
   → If no clear user flow: ERROR "Cannot determine user scenarios"
5. Generate Functional Requirements
   → Each requirement must be testable
   → Mark ambiguous requirements
6. Identify Key Entities (if data involved)
7. Run Review Checklist
   → If any [NEEDS CLARIFICATION]: WARN "Spec has uncertainties"
   → If implementation details found: ERROR "Remove tech details"
8. Return: SUCCESS (spec ready for planning)
```

---

## ⚡ Quick Guidelines - Full-Stack Development
- ✅ Focus on WHAT users need and WHY (ビジネス価値重視)
- ❌ Avoid HOW to implement (実装詳細は計画フェーズで)
- 👥 Written for business stakeholders, not developers
- 🌐 Consider both frontend UX and backend data flows
- 📱 Multi-platform considerations (Web, Mobile, API)

### Section Requirements
- **Mandatory sections**: Must be completed for every feature
- **Optional sections**: Include only when relevant to the feature
- When a section doesn't apply, remove it entirely (don't leave as "N/A")
- **Full-Stack Context**: Consider both user-facing features and data processing needs

### For AI Generation
When creating this spec from a user prompt:
1. **Mark all ambiguities**: Use [NEEDS CLARIFICATION: specific question] for any assumption you'd need to make
2. **Don't guess**: If the prompt doesn't specify something (e.g., "login system" without auth method), mark it
3. **Think like a tester**: Every vague requirement should fail the "testable and unambiguous" checklist item
4. **Common underspecified areas in Full-Stack projects**:
   - User types and permissions (RBAC requirements)
   - Data retention/deletion policies (GDPR compliance)
   - Performance targets and scale (concurrent users, data volume)
   - Error handling behaviors (frontend + backend)
   - Integration requirements (APIs, third-party services)
   - Security/compliance needs (authentication, authorization)
   - Multi-language support (i18n/l10n)
   - Cross-platform compatibility (browsers, devices)

---

## User Scenarios & Testing *(mandatory)*

### Primary User Story
[Describe the main user journey in plain language]

### Acceptance Scenarios
1. **Given** [initial state], **When** [action], **Then** [expected outcome]
2. **Given** [initial state], **When** [action], **Then** [expected outcome]

### Edge Cases
- What happens when [boundary condition]?
- How does system handle [error scenario]?

## Requirements *(mandatory)*

### Functional Requirements
- **FR-001**: System MUST [specific capability, e.g., "allow users to create accounts"]
- **FR-002**: System MUST [specific capability, e.g., "validate email addresses"]  
- **FR-003**: Users MUST be able to [key interaction, e.g., "reset their password"]
- **FR-004**: System MUST [data requirement, e.g., "persist user preferences"]
- **FR-005**: System MUST [behavior, e.g., "log all security events"]

*Example of marking unclear requirements:*
- **FR-006**: System MUST authenticate users via [NEEDS CLARIFICATION: auth method not specified - email/password, SSO, OAuth?]
- **FR-007**: System MUST retain user data for [NEEDS CLARIFICATION: retention period not specified]

### Non-Functional Requirements *(Full-Stack considerations)*
- **NFR-001**: Performance - [e.g., "API responses < 200ms, Page load < 3s"]
- **NFR-002**: Scalability - [e.g., "Support 1000 concurrent users"]
- **NFR-003**: Security - [e.g., "HTTPS only, password hashing, OWASP compliance"]
- **NFR-004**: Availability - [e.g., "99.9% uptime, graceful degradation"]
- **NFR-005**: Compatibility - [e.g., "Chrome/Firefox/Safari, iOS/Android"]

### Integration Requirements *(if applicable)*
- **IR-001**: External APIs - [e.g., "Payment gateway integration"]
- **IR-002**: Data Sources - [e.g., "Connect to existing customer database"]
- **IR-003**: Third-party Services - [e.g., "Email service, file storage"]

### Key Entities *(include if feature involves data)*
- **[Entity 1]**: [What it represents, key attributes without implementation]
- **[Entity 2]**: [What it represents, relationships to other entities]
- **[Entity 3]**: [Cross-language data consistency requirements]

---

## Review & Acceptance Checklist
*GATE: Automated checks run during main() execution*

### Content Quality
- [ ] No implementation details (languages, frameworks, APIs)
- [ ] Focused on user value and business needs
- [ ] Written for non-technical stakeholders
- [ ] All mandatory sections completed

### Requirement Completeness
- [ ] No [NEEDS CLARIFICATION] markers remain
- [ ] Requirements are testable and unambiguous  
- [ ] Success criteria are measurable
- [ ] Scope is clearly bounded
- [ ] Dependencies and assumptions identified

---

## Execution Status
*Updated by main() during processing*

- [ ] User description parsed
- [ ] Key concepts extracted
- [ ] Ambiguities marked
- [ ] User scenarios defined
- [ ] Requirements generated
- [ ] Entities identified
- [ ] Review checklist passed

---
