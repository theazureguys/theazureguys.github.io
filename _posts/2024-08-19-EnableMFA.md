---
title: Enable MFA on your Azure Tenant Before 15th Oct 2024
date: 2024-08-19 15:42:05 +/-TTTT
categories: [Azure, Entra, MFA]
tags: [azure, entra, id, mfa] # TAG names should always be lowercase
---

Starting from the 15th of October 2024, Microsoft will be enforcing multifactor authentication (MFA) to sign into the <a href="https://portal.azure.com/" target="_blank">Azure portal</a>, Microsoft <a href="https://entra.microsoft.com/" target="_blank">Entra admin center</a>, and <a href="https://intune.microsoft.com/" target="_blank">Intune admin center</a>.

> To ensure you/your users maintain access, you’ll need to enable MFA by the **15th of October 2024**.
{: .prompt-warning }

Guidance for enabling MFA can be found <a href="https://learn.microsoft.com/en-gb/entra/identity/authentication/concept-mandatory-multifactor-authentication" target="_blank">here</a>.

## Enforcement Phases

- **Phase 1**: Starting in the second half of 2024, MFA will be required to sign in to the Azure portal, Microsoft Entra admin center, and Microsoft Intune admin center. The enforcement will gradually roll out to all tenants worldwide. This phase won't impact other Azure clients such as Azure CLI, Azure PowerShell, Azure mobile app, or IaC tools. 

- **Phase 2**: Beginning in early 2025, MFA enforcement gradually begins for sign in to Azure CLI, Azure PowerShell, Azure mobile app, and IaC tools. Some customers may use a user account in Microsoft Entra ID as a service account. It's recommended to migrate these user-based service accounts to secure cloud based service accounts with workload identities.