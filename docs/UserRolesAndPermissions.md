# User Roles

The types of users in the system.

* Anonymous : Any visitor to the site that is not authenticated.
* Participant : A disabled person who is elegible for Dcheme benefits.
* Carer : A person (usually a family member) that cares for the participant.
* Provider : A registered disability service provider organisation that provides products or services to participants.
* SupportWorker : A person (who may be employed by a provider) that directly provides support to a participent (eg home help).
* Planner : An NDIS employee or agent that creates fair and reasonable support plan for registered participants.
* PlanManager : A person (often a book-keeper) that helps self-managed participants deal with regulatory obligations such as payroll.
* Administrator : An NDIS employee that performs system level administration work.

# Resources

The protected resources in the system over which users may have some permissions.

* SupportItem : A type of disability product or service that the NDIS will fund for eligible participants.
* Plan : A list of support items (with quantities) that represents a "fair and reasonable" set of supports for a particpant in a given year. This is essentially the annual budget for a participant.
* Participent : The information record about a particular participent.
* ProviderOrg : A provider organisation and related attributes.
* Service : An actual product or service offered by a provider organisation and listed on the e-market.
* ServiceRequest : A request for a product or service issued from a particpant to a provider.
* Acquittal : A time record or goods receipt that represents confirmation that the request service was delivered.
* Payment : The payment for a requested product or service.
* Account : A register of financial and non-financial transactions made by a participant (or carer) under a plan.  

# Permissions

The allowed actions that each role can perform on each resource. Actions are expressed as CRUD (REST) Verbs.
* C : Create (POST)
* R : Read (GET)
* U : Update (PUT)
* D : Delete (DELETE)
* - : No permission

| Role / Resource | Anon | Participant | Carer | Provider | Support Worker | Planner | Plan Manager | Admin |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SupportItem | R | R | R | R | R | R | R | CRUD |
| Plan | - | R | R | - | - | CRUD | R | R |
| Participent | - | CRUD | CRUD | - | - | R | R | R |
| ProviderOrg | - | - | - | CRUD | R | R | - | CRUD |
| Service | R | R | R | CRUD | R | R | R | CRUD |
| ServiceRequest | - | CRUD | CRUD | RU | R | R | R | RUD |
| Acquittal | - | CRUD | CRUD | RU | RU | R | RU | CRUD |
| Payment | - | CR | CR | R | R | R | CR | CR |
| Account | - | R | R | - | - | R | R | R |

# Scope Rules

The scope of resources over which the role permission applies.

* Participants can only see their own profile, plan, account, and transactions.
* Carers can see all resources related to participents for which they are the registered carer.
* Providers can only see their own profile, services, account, and transactions.
* SupportWorkers can only see ServiceRequests and acquittals in which they are the subject.
* Planners can see any participant plan
* PlanManagers can only see plans, accounts, and transactions for participents for which they are the registered plan manager
* Administrators can see all resources.



# Authentication Model

All users will be authenticated from an external OIDC or SAML provider.
* In the prototype system, use Google OIDC.
* In production:
   * Government staff (admin & planner) will authenticate using [VANguard SAML FAS](http://vanguard.business.gov.au/ourservices/Pages/Federated-Authentication-Service-(FAS).aspx)
   * Business staff (provider, plan manager) will authenticate using [VANguard OIDC UAS](http://vanguard.business.gov.au/ourservices/Pages/User-Authentication-Service-(UAS).aspx)
   * Individuals (participents, carers) will authenticate using [myGov OIDC](https://www.humanservices.gov.au/customer/subjects/about-mygov)

