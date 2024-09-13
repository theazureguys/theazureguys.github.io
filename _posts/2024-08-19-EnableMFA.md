---
title: Enable MFA on your Azure Tenant Before 15th Oct 2024
date: 2024-08-19 15:42:05 +/-TTTT
categories: [Azure, Entra, MFA]
tags: [azure, entra, id, mfa, security] # TAG names should always be lowercase
---

Starting from the 15th of October 2024, Microsoft will be enforcing multifactor authentication (MFA) to sign into the <a href="https://portal.azure.com/" target="_blank">Azure portal</a>, Microsoft <a href="https://entra.microsoft.com/" target="_blank">Entra admin center</a>, and <a href="https://intune.microsoft.com/" target="_blank">Intune admin center</a>.

> To ensure you/your users maintain access, you’ll need to enable MFA by the **15th of October 2024**.
{: .prompt-warning }

Microsoft is making these preconfigured security settings available to everyone, because we all know managing security can be difficult. Based on our learnings more than 99.9% of those common identity-related attacks are stopped by using multifactor authentication and blocking legacy authentication.

> Microsoft's goal is to ensure that all organizations have at least a basic level of security enabled at ***no extra cost***.
{: .prompt-tip }

## Enforcement Phases

- **Phase 1**: Starting in the second half of 2024, MFA will be required to sign in to the Azure portal, Microsoft Entra admin center, and Microsoft Intune admin center. The enforcement will gradually roll out to all tenants worldwide. This phase won't impact other Azure clients such as Azure CLI, Azure PowerShell, Azure mobile app, or IaC tools. 

- **Phase 2**: Beginning in early 2025, MFA enforcement gradually begins for sign in to Azure CLI, Azure PowerShell, Azure mobile app, and IaC tools. Some customers may use a user account in Microsoft Entra ID as a service account. It's recommended to migrate these user-based service accounts to secure cloud based service accounts with workload identities.

## Enable Basic Entra ID MFA, No Entra ID Premium License Required

You can enable Basic Entra ID MFA without the need for a Premium Entra License.

Open the Azure Portal:

1. Go to the "Microsoft Entra ID" module
2. Under "Manage" section, go to "Properties"
3. On the "Properties" blade, scroll down and under "Security Defaults" you will see a link for "Manage security defaults"
4. Click "Manage security defaults", it opens a blade on the right with a drop down, with enable and disable options
5. Select "enable" and save, at the bottom

Basic MFA is now enabled, no license required.

![image](/assets/img/enablemfa/img_1.png)

Bear in mind that this is the Basic MFA option so is not as configurable, in terms of exclusions, conditional access etc. For further functionality, you will need a <a href="https://www.microsoft.com/en-gb/security/business/microsoft-entra-pricing" target="_blank">Premium license</a>.

Further guidance for enabling MFA with more features can be found <a href="https://learn.microsoft.com/en-gb/entra/identity/authentication/concept-mandatory-multifactor-authentication" target="_blank">here</a>.