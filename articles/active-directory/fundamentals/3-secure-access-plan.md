---
title: Create a security plan for external access to Azure Active Directory 
description: Plan the security for external access to your organization's resources.
services: active-directory
author: gargi-sinha
manager: martinco
ms.service: active-directory
ms.workload: identity
ms.subservice: fundamentals
ms.topic: conceptual
ms.date: 12/15/2022
ms.author: gasinh
ms.reviewer: ajburnle
ms.custom: "it-pro, seodec18"
ms.collection: M365-identity-device-management
---

# Create a security plan for external access 

Before you create an external-access security plan, ensure the following conditions are met.

* [Determine your security posture for external access](1-secure-access-posture.md)
* [Discover the current state of external collaboration in your organization](2-secure-access-current-state.md)

For your security plan, document the following information:

* Applications and resources to be grouped for access
* Sign-in conditions for external users
  * Device state, sign-in location, client application requirements, and user risk
* Policies that determine when to review and remove access
* User populations to be grouped for a similar experience

After you document the information, use Microsoft identity and access management policies, or another identity provider (IdP) to implement the plan.

## Resources to be grouped for access

To group resources for access: 

* Microsoft Teams groups files, conversation threads, and other resources. Formulate an external access strategy for Microsoft Teams.
  * See, [Secure external access to Microsoft Teams, SharePoint, and OneDrive for Business](9-secure-access-teams-sharepoint.md)
* Use entitlement management access packages to create and delegate management of packages of applications, groups, teams, SharePoint sites, etc. 
  * [Create a new access package in entitlement management](/azure/active-directory/governance/entitlement-management-access-package-create) 
* Apply Conditional Access policies to up to 250 applications, with the same access requirements
  *  [What is Conditional Access?](/azure/active-directory/conditional-access/overview) 
* Use Cross Tenant Access Settings Inbound Access to define access for application groups of external users 
  *  [Overview: Cross-tenant access with Azure AD External Identities](/azure/active-directory/external-identities/cross-tenant-access-overview) 

Document the applications to be grouped. Considerations include:

* **Risk profile** - Assess the risk if a bad actor gains access to an application. 
  * Identify application as high, medium, or low risk. Avoid grouping high-risk with low-risk.
  * Document applications that can't be shared with external users
* **Compliance frameworks** - Determine compliance frameworks for apps
  * Identify access and review requirements
* **Applications for roles or departments** - Assess applications to be grouped for a role or department access
* **Collaboration applications** - Identify collaboration applications external users can access, such as Teams and SharePoint
  * For productivity applications, external users might have licenses, or you might provide access

For application and resource group access by external users, document the following information:

* Descriptive group name, for example High_Risk_External_Access_Finance 
* Applications and resources in the group
* Application and resource owners and contact information
* Access is controlled by IT, or delegated to a business owner
* Prerequisites for access: background check, training, etc.
* Compliance requirements to access resources
* Challenges, for example multi-factor authentication (MFA) for some resources
* Cadence for reviews, by whom, and where it's documented

> [!TIP]
> Use this type of governance plan for internal access.

## Document sign-in conditions for external users

Determine the sign-in requirements for external users who request access. Base requirements on the resource risk profile, and the user's risk assessment during sign-in. Configure sign-in conditions using Conditional Access: a condition and an outcome. For example, you can require MFA.

Learn more: [What is Conditional Access?](../conditional-access/overview.md)

**Resource risk-profile sign-in conditions**

Consider the following risk-based policies to trigger MFA.

* **Low** - MFA for some application sets
* **Medium** - MFA when other risks are present
* **High** - External users always use MFA

Learn more: 

* [Tutorial: Enforce multi-factor authentication for B2B guest users](../external-identities/b2b-tutorial-require-mfa.md)
* Trust MFA from external tenants
  * See, [Configure cross-tenant access settings for B2B collaboration, Modify inbound access settings](../external-identities/cross-tenant-access-settings-b2b-collaboration.md#modify-inbound-access-settings)

### User and device sign-in conditions

Use the following table to help assess policy to address risk.

| User or sign-in risk| Proposed policy |
| --- | --- |
| Device| Require compliant devices |
| Mobile apps| Require approved apps |
| Identity protection is high risk| Require user to change password |
| Network location| To access confidential projects, require sign-in from an IP address range |

To use device state as policy input, the device is registered or joined to your tenant. Configure cross-tenant access settings must be configured to trust the device claims from the home tenant. See, [Modify inbound access settings](../external-identities/cross-tenant-access-settings-b2b-collaboration.md#modify-inbound-access-settings).

You can use identity-protection risk policies. However, mitigate issue in the user home tenant. See, [Common Conditional Access policy: Sign-in risk-based multifactor authentication](../conditional-access/howto-conditional-access-policy-risk.md).

For network locations, you can restrict access to IP addresses ranges you own. Use this method if external partners access applications while at your location. See, [Conditional Access: Block access by location](../conditional-access/howto-conditional-access-policy-location.md)

## Document access review policies

Document policies that dictate when to review resource access, and remove account access for external users. Inputs might include:

* Compliance frameworks requirements
* Internal business policies and processes
* User behavior

Your policies will be customized, however consider the following parameters:

* **Entitlement management access reviews**:
  * [Change lifecycle settings for an access package in entitlement management](../governance/entitlement-management-access-package-lifecycle-policy.md)
  * [Create an access review of an access package in entitlement management](../governance/entitlement-management-access-reviews-create.md)
  * [Add a connected organization in entitlement management](../governance/entitlement-management-organization.md): group users from a partner and schedule reviews
* **Microsoft 365 groups**: 
  * [Microsoft 365 group expiration policy](/microsoft-365/solutions/microsoft-365-groups-expiration-policy?view=o365-worldwide&preserve-view=true)
* **Options**: 
  * If external users don't use access packages or Microsoft 365 groups, determine when accounts become inactive or deleted
  * Remove sign-in for accounts that don't sign in for 90 days
  * Regularly assess access for external users

## Access control methods

Some features, for example entitlement management, are available with an Azure AD Premium 2 (P2) license. Microsoft 365 E5 and Office 365 E5 licenses include Azure AD P2 licenses. 

Other combinations of Microsoft 365, Office 365, and Azure AD have functionality to manage external users. See, [Microsoft 365 guidance for security & compliance](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance).

> [!NOTE]
> Licenses are for one user. Therefore users, administrators, and business owners can have delegated access control. This scenario can occur with Azure AD P2 or Microsoft 365 E5, and you don't have to enable licenses for all users. The first 50,000 external users are free. If you don't enable P2 licenses for other internal users, they can't use entitlement management. 

## Govern access with Azure AD P2 and Microsoft 365 or Office 365 E5

Azure AD P2 and Microsoft 365 E5 have all the security and governance tools.

### Provision, sign-in, review access, and deprovision access

Entries in bold are recommended.

| Feature| Provision external users| Enforce sign-in requirements| Review access| Deprovision access |
| - | - | - | - | - |
| Azure AD B2B collaboration| Invite via email, one-time password (OTP), self-service|N/A| **Periodic partner review**| Remove account<br>Restrict sign-in |
| Entitlement management| **Add user by assignment or self-service access**|N/A| Access reviews|**Expiration of, or removal from, access package**|
| Office 365 groups|N/A|N/A| Review group memberships| Group expiration or deletion<br> Removal from group |
| Azure AD security groups|N/A| **Conditional Access policies**: Add external users to security groups as needed|N/A| N/A|

### Resource access 
 
Entries in bold are recommended.

|Feature | App and resource access| SharePoint and OneDrive access| Teams access| Email and document security |
| - |-|-|-|-|
| Entitlement management| **Add user by assignment or self-service access**| **Access packages**| **Access packages**| N/A|
| Office 365 Group|N/A | Access to site(s) and group content| Access to teams and group content|N/A|
| Sensitivity labels|N/A| **Manually and automatically classify and restrict access**| **Manually and automatically classify and restrict access**| **Manually and automatically classify and restrict access** |
| Azure AD security groups| **Conditional Access policies for access not included in access packages**|N/A|N/A|N/A|

### Entitlement management 

Use entitlement management to provision and deprovision access to groups and teams, applications, and SharePoint sites. Define the connected organizations allowed access, self-service requests, and approval workflows. To ensure access ends correctly, define expiration policies and access reviews for packages. 

Learn more: [Create a new access package in entitlement management](../governance/entitlement-management-access-package-create.md) 

## Governance with Azure AD P1, Microsoft 365, Office 365 E3

### Provision, sign-in, review access, and deprovision access

Items in bold are recommended.

|Feature | Provision external users| Enforce sign-in requirements| Review access| Deprovision access |
| - |-|-|-|-|
| Azure AD B2B collaboration| **Invite by email, OTP, self-service**| Direct B2B federation| **Periodic partner review**| Remove account<br>Restrict sign-in |
| Microsoft 365 or Office 365 groups|N/A|N/A|N/A|Group expiration or deletion<br>Removal from group |
| Security groups|N/A| **Add external users to security groups (org, team, project, etc.)**|N/A| N/A|
| Conditional Access policies|N/A| **Sign-in Conditional Access policies for external users**|N/A|N/A|

### Resource access

|Feature | App and resource access| SharePoint and OneDrive access| Teams access| Email and document security |
| - |-|-|-|-|
| Microsoft 365 or Office 365 groups|N/A| **Access to group site(s) and associated content**|**Access to Microsoft 365 group teams and associated content**|N/A|
| Sensitivity labels|N/A| Manually classify and restrict access| Manually classify and restrict access| Manually classify to restrict and encrypt |
| Conditional Access policies| Conditional Access policies for access control|N/A|N/A|N/A|
| Other methods|N/A| Restrict SharePoint site access with security groups<br>Disallow direct sharing| **Restrict external invitations from a team**|N/A|

### Next steps

* [Determine your security posture for external access](1-secure-access-posture.md)
* [Discover the current state of external collaboration in your organization](2-secure-access-current-state.md)
* [Securing external access with groups](4-secure-access-groups.md)
* [Transition to governed collaboration with Azure Active Directory B2B collaboration](5-secure-access-b2b.md)
* [Manage external access with entitlement management](6-secure-access-entitlement-managment.md)
* [Secure access with Conditional Access policies](7-secure-access-conditional-access.md)
* [Control access with sensitivity labels](8-secure-access-sensitivity-labels.md)
* [Secure external access to Microsoft Teams, SharePoint, and OneDrive for Business](9-secure-access-teams-sharepoint.md)
