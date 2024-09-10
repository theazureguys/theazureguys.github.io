---
title: Azure Public IPs are now zone-redundant by default
date: 2024-09-10 11:42:05 +/-TTTT
categories: [Azure, Network, IPs]
tags: [azure, network, ip, zone, redundant] # TAG names should always be lowercase
---

 Microsoft Azure Public IPs are zone-redundant by default. This means that unless you specifically select a single zone when deploying your Microsoft Azure Standard Public IPs, they will be zone-redundant—without any extra steps on your part. Yes, automatically.

If you don’t select a zone for your Standard Public IPs (such as the default way of creating one), you will now get the benefits of zone redundancy—at no extra cost. A zone-redundant IP is created in three zones for a region and can survive any single zone failure, improving the resiliency of your application using this public IP.

## Which regions is this available in?

Zone redundancy by default for public IPs is available in 12 regions (At the time of writing this post) and will continue to expand in the upcoming months. The goal is to ensure that all regions get this benefit. This will be an incremental process and today the following regions have this available:

- Central Canada
- Central Poland
- Central Israel
- Central France
- Central Qatar
- East Norway
- Italy North
- Sweden Central
- South Africa North
- South Brazil
- West Central Germany
- West US 2

This post will not be updated as we add more regions. For an up-to-date region list, please refer to the <a href="https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/public-ip-addresses#availability-zone" target="_blank">Public IP documentation</a>.

## What do I need to do to get the benefits?

If you have Standard Public IPs with no zone parameters, you don’t need to take any action. Your IPs are already zone-redundant in the regions below. If you already have zone-redundant IPs, they will continue to stay zone-redundant. Whether you create your Public IPs today or created them years ago, this applies to all of your Standard public IPs.

If you upgrade your Basic SKU Public IP to Standard SKU, with this announcement, it will now be zone-redundant. No extra steps or actions are needed apart from the upgrade.

## Further Details

For more info, check out the announcement on the <a href="https://azure.microsoft.com/en-us/blog/azure-public-ips-are-now-zone-redundant-by-default/" target="_blank">MSFT Blog</a>.