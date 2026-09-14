Gabriel Chinchilla Villalobos

Software Engineer — Authentication & Identity and Access Management Alajuela, Costa Rica

I build and operate secure web applications, with a focus on authentication, authorization and access management on Microsoft Entra ID (Azure AD). Nine years of experience, seven of them at Microsoft.

About this profile

Most of my production work over the last seven years was on internal Microsoft platforms, so the code isn't public and never will be. This profile is intentionally light as a result — the summaries below describe what I actually built, and I'm happy to walk through architecture, trade-offs and failure modes in detail.

What I work on
Authentication flows — OpenID Connect, OAuth 2.0 (authorization code, On-Behalf-Of, client credentials), Single Sign-On through Azure AD, session management
Token security — JWT issuance and validation, token lifetime management, claims-based authorization, API token validation
Access management — MFA enforcement, conditional access, Just-In-Time provisioning, RBAC, FIDO2 / YubiKey enrollment
Zero-secret architecture — managed identities and Key Vault-held certificates for service-to-service authentication, so nothing lives in configuration
Secure development — threat modeling, OWASP Top 10 review, CodeQL static analysis in CI, vulnerability triage
Tech

Languages — C# (primary), JavaScript, TypeScript, Python, PowerShell, Bash, Java Frameworks — .NET Core, .NET MVC, Blazor Server, Node.js, Vue.js, Entity Framework Azure — App Service, Functions, Container Apps, Entra ID, Key Vault, Service Bus, Event Grid, Cosmos DB, Azure Monitor, Virtual Networks Data — Cosmos DB, SQL Server, KQL, NoSQL Infrastructure — ARM, Bicep, Terraform, Azure DevOps Pipelines, Git, CI/CD, Kubernetes (Helm, namespaces, scheduling controls)

Selected work

Internal Microsoft projects. Not public, described here for context.

Lab-Box — Azure deployment and training platform

End-to-end management of Azure ARM template deployments with pre-packaged troubleshooting scenarios for support engineer training.

Implemented authentication twice over — a manual OpenID Connect implementation and an Azure Easy Auth integration — using the OAuth 2.0 On-Behalf-Of flow to read user identity from the ID token
Designed a token management system validating request authenticity and authorization, blocking unauthorized access and duplicate processing
Scaled to 12,000+ template launches by 2,600+ users in six months, cutting request processing time by 50%
Replaced scraping-based tracking with event-driven ingestion over Azure Service Bus and idempotent processing — 90% reduction in duplicate records and execution time
SME Ramp-Up — global onboarding platform

Standardized subject matter expert onboarding across global support teams.

Entra ID authentication with RBAC authorization, built to stay agnostic to both the hosting environment and the identity provider
Adopted by 700+ users, used to qualify 150+ engineers
Cut memory consumption from 8 GB to 4 GB through a revised caching strategy
PeopleMappingV2 — layered HR data service

Multi-service application for custom human resources data.

Access restricted to trusted sources via Azure Virtual Network policies plus token-based authentication over the OAuth 2.0 On-Behalf-Of flow
.NET backend APIs exposed through OpenAPI to a Blazor client, serving 700+ records in under 3 seconds via a custom caching layer
Refactored a monolith into reusable service components behind versioned OpenAPI endpoints
Education & certifications

B.Sc. Computational Systems Engineering — Universidad Fidélitas (2015–2018) Post-Bachelor Licentiate, Systems Quality Engineering — Universidad Fidélitas (in progress)

Microsoft Certified: Identity and Access Administrator Associate (SC-300) — in progress
Microsoft Certified: Azure Administrator Associate (AZ-104)
Microsoft Certified: Azure Fundamentals (AZ-900)
Microsoft Certified: Azure AI Fundamentals (AI-900)
Microsoft Certified: GitHub Foundations
Contact

LinkedIn · gab-ch9@outlook.com

English (professional) · Spanish (native) · Portuguese (beginner)
