<h1>Gabriel Chinchilla Villalobos</h1>

**Software Engineer, secure, cost-efficient cloud services**

📍 Alajuela, Costa Rica · open to remote
[LinkedIn](https://www.linkedin.com/in/gabrielchinchillavillalobos/) - [Email](mailto:gab-ch9@outlook.com)

<h3>About this profile</h3>
<hr/>
Systems engineer with 10 years in tech, the last 3 building internal automation and engineering platforms at Microsoft on .NET and Azure. I focus on secure-by-default services (managed identities, least privilege, no secrets in config) that stay cheap and fast in shared subscriptions.

Most of my production work was on internal Microsoft platforms, so the code isn't public and never will be. The summaries below describe what I actually built, and I'm happy to walk through architecture, trade-offs and failure modes in detail. These projects co-lived in the same subscription with multiple other resources so managing cost and performance was imperative 

Have a look at the projects I worked on for a direct description of what I did.

<h3>Projects</h3>
<hr/>

### Labbox: on-demand troubleshooting labs
Event-driven platform that deploys community-authored ARM templates as live troubleshooting labs, delivered to the engineer's Azure portal in under 10 seconds.
- **Scale:** 12,000+ labs deployed over 6 months at a 98% success rate
- **Architecture:** Split a monolithic function into single-responsibility functions, and replaced post-deployment scraping with event-driven telemetry through Service Bus and idempotent processing, cutting duplicate records and execution time by 90%
- **Performance:** Processing time reduced 50%; Cosmos DB for low-latency ingestion, KQL for telemetry analysis
- **My role:** Design, development, testing, documentation and production support
- **Stack:** .NET, Azure Functions, Service Bus, ARM, Cosmos DB, KQL, OAuth2
- **Key decision:** Removal of monolithic function to split functions to achieve single-responsibility principle. Change from scrapping post-deployment telemetry collection to event-based

### SMERamp: global SME selection and promotion platform
Replaced a spreadsheet-and-nomination process (no documented criteria, hand-picked candidates, no performance data) with a single data-driven pipeline for selecting and promoting Subject Matter Experts across regions.

- **Scale:** 700+ users; 150+ qualifying engineers identified and selected
- **My role:** Sole owner: design, development, testing, documentation and production support
- **Contribution signals:** ADO wiki contributions pulled through the ADO REST API, plus Teams channel activity, positive survey responses and case-resolution correlation, surfaced in a Power BI dashboard for candidate review
- **Security:** Custom RBAC with time-boxed grants checked on every request, JWT revalidation and IP restrictions, caller identity derived from the validated token (no BOLA surface), and an audit trail for every permission change
- **Performance & cost:** Moved connection handling from per-scope to singleton clients, trimmed server-side caching and offloaded user-info calls to a dedicated API. Memory went from spiky 8 GB peaks to a stable profile, and the App Service plan dropped to 4 GB
- **Outcome:** Quarterly SME promotions rose sharply under a documented, cross-region process, with standardized criteria and observability where there had been none
- **Stack:** .NET, Blazor Server, App Service, Entra ID, managed identity, Cosmos DB, Azure Data Explorer (Kusto), ADO REST API, Power BI

### PeopleMapping: HR data platform and shared identity API
Rebuilt a Power Apps HR tool as a modern web app backed by an identity API designed for reuse across the org's tools. I proposed and advocated this approach internally so teams would share one secure surface for user data and authorization instead of re-implementing it.

- **My role:** Design, development, testing, documentation and production support. I prototyped several front ends (including React) before settling on Blazor Server, which was possible because all business logic lives behind the API.
- **Shared identity API:** Versioned OpenAPI service for user lookup and authorization. Each consuming app authenticates with managed identity and federated credentials on its own app registration, scoped to only the operations it needs, with no client secrets anywhere. The signed-in user's identity is verified on every call to decide what that person may do.
- **Zero-trust enforcement:** Bearer tokens validated in middleware as a single choke point; deny-by-default authorization; group-based roles; the caller comes from the validated token, never from a parameter; network access locked down with VNet integration.
- **Security reviews:** Passed Microsoft Secure Future Initiative (SFI) and SDL threat modeling reviews.
- **Data layer:** Built a lightweight ORM-style mapper for KQL that turns raw `IDataReader` results into strongly typed, schema-based objects.
- **Observability:** Per-app telemetry on who calls what, top consumers and query performance, tracked in Grafana and Azure dashboards.
- **Performance:** Custom caching brought load time for 700+ records under 3 seconds.
- **Business impact:** Management can add their own data fields alongside the HR source without needing HR approval to change base records. The two datasets coexist cleanly.
- **Stack:** .NET, Blazor Server, ASP.NET Core Web API (OpenAPI), Azure Data Explorer(KQL), App Service with Easy Auth, Entra ID, managed identity and federated credentials, Microsoft Graph, VNet, Grafana

### Wiki-Usage: wiki analytics pipeline
Daily pipeline that measures how the Azure VM support team's ADO wikis are actually used, so improvement work goes to the articles that matter most.

- **How it works:** An ADO pipeline triggers an Azure Function on schedule and gates on its response (200 = complete, anything else fails the run). The function walks every wiki through the ADO REST API with continuation tokens and recursive page discovery, and fans out across parallel workers on the Flex Consumption plan.
- **Performance:** Full wiki estate processed in ~5 minutes per run.
- **Output:** Page usage telemetry and content loaded into Kusto via queued ingestion, powering daily usage indicators cross-referenced with case resolution to rank which articles need rework.
- **Efficiency:** Event-driven, pay-per-execution compute with no idle cost; queued ingestion keeps cluster load low where real-time freshness isn't needed.
- **Security:** Managed identity for ADO and Kusto access, with no stored credentials.
- **Stack:** Python, Azure Functions (Flex Consumption), Azure DevOps Pipelines, ADO REST API, Azure Data Explorer (KQL), managed identity

### Wiki-Redirect: SME escalation tracking
Lightweight Azure Function that measures which wiki articles send engineers to SMEs, exposing the documentation gaps behind escalations.

- **How it works:** SME contact links in the wikis point to the function. It requires an authenticated request, logs who clicked and from which article, then redirects the engineer to the right Teams channel. The user sees one seamless click.
- **Security:** Redirects only to an allowlist of approved Teams destinations, so the endpoint can't be abused as an open redirect.
- **Output:** Ranking of articles that drive the most SME transfers, used to prioritize rewrites and fill missing information.
- **Efficiency:** Runs only per click on consumption compute. Telemetry uses Kusto queued ingestion because instant availability isn't needed, which saves cluster resources.
- **Stack:** C#/.NET, Azure Functions, Entra ID authentication, Azure Data Explorer (KQL, queued ingestion), Microsoft Teams deep links

<h3>What I work on</h3>
<hr/>

**1. Authentication flows:** OpenID Connect, OAuth 2.0 (authorization code, On-Behalf-Of, client credentials), Single Sign-On through Azure AD, session management
**2. Token security:** JWT issuance and validation, token lifetime management, claims-based authorization, API token validation
**3. Access management:** MFA enforcement, conditional access, Just-In-Time provisioning, RBAC, FIDO2
**4. Zero-secret architecture:** managed identities and Key Vault-held certificates for service-to-service authentication, so nothing lives in configuration
**5. Secure development:** threat modeling, OWASP Top 10 review, CodeQL static analysis in CI, vulnerability triage
**6. Clean code:** Reusable, understandable and maintanable code
**7. UI:** UIs compliant with accessibility standards with responsive design in mind

<h3>Tech stack</h3>
<hr/>

- **Languages:** C#, TypeScript, JavaScript, Python, SQL, KQL
- **Backend:** .NET Core, ASP.NET MVC, Blazor Server, Entity Framework, Node.js, REST/OpenAPI
- **Frontend:** Vue.js
- **Azure:** App Service, Functions, Container Apps, Service Bus, Event Grid, Entra ID, Key Vault, Monitor, VNets
- **Data:** SQL Server, Cosmos DB
- **IaC & DevOps:** Bicep, ARM, Terraform, Azure DevOps Pipelines, GitHub Actions/CodeQL, Kubernetes (Helm)

<h3>Education and certifications</h3>
<hr/>

B.Sc. Computational Systems Engineering — Universidad Fidélitas (2015–2018) Post-Bachelor Licentiate, Systems Quality Engineering — Universidad Fidélitas (in progress)
Microsoft Certified: Identity and Access Administrator Associate (SC-300) — in progress
Microsoft Certified: Azure Administrator Associate (AZ-104)
Microsoft Certified: Azure Fundamentals (AZ-900)
Microsoft Certified: Azure AI Fundamentals (AI-900)
Microsoft Certified: GitHub Foundations

<h3>Spoken languages:</h3> 
<hr/>

English (professional) - Spanish (native) - Portuguese (beginner)
