---
title: Microsoft Exchange compatibility with Single Label Domains, Disjointed Namespaces, and Discontiguous Namespaces
description: Describes compatibility of Microsoft products with Single Label Domains, Disjoint Namespaces, and Discontiguous Namespaces.
ms.date: 09/14/2020
author: Deland-Han
ms.author: delhan
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: jarrettr, kaushika
ms.prod-support-area-path: DNS
ms.technology: Networking
---
# Microsoft Exchange compatibility with Single Label Domains, Disjointed Namespaces, and Discontiguous Namespaces

This article describes the compatibility of Microsoft Exchange with Single Label Domains, Disjoint Namespaces, and Discontiguous Namespaces.

_Original product version:_ &nbsp;Windows Server 2012 R2  
_Original KB number:_ &nbsp;2269838


## More information

### Single Label Domains

For a description of Single Label Domains, see the Single Label Domains topic in the [Microsoft DNS Namespace Planning Solution Center.](/troubleshoot/windows-server/networking/dns-namespace-design) 

### Disjoint Namespaces

For a description of Disjoint Namespaces, see the Disjoint Namespaces topic in the [Microsoft DNS Namespace Planning Solution Center.](/troubleshoot/windows-server/networking/dns-namespace-design) 

### Discontiguous Namespaces

For a description of Discontiguous Namespaces, also known as a non-contiguous namespaces, see the Discontiguous Namespaces topic in the [Microsoft DNS Namespace Planning Solution Center.](/troubleshoot/windows-server/networking/dns-namespace-design)


### Exchange Server

In response to customer feedback, the Exchange team has updated its testing matrix and has determined that Exchange Server 2010 will be supported on SLDs, Disjoint Namespaces, and Discontiguous Namespaces. This page contains a brief description of each of these scenarios and special considerations. If you intend to install Exchange 2010 into one of these environments, read the [Exchange Team Blog's documentation](http://msexchangeteam.com/archive/2009/10/27/452969.aspx) about the applicable subject.

> [!NOTE]
> For information about disjoint namespace scenarios in Microsoft Exchange Server 2013, visit the following TechNet website:

[Disjoint namespace scenarios](https://technet.microsoft.com/library/bb676377%28v=exchg.150%29.aspx) 

In adding support for these types of topologies, there's an underlying requirement for DNS to be correctly installed and configured. Before users continue with any deployment that is defined here, clients and servers must be able to reliably resolve DNS queries for a given resource in the appropriate namespace.

#### Single Label Domains

Although Exchange 2010 is supported with SLDs, the Exchange product team's view is that SLDs aren't a recommended configuration and may not be supported by future Exchange versions. Other Microsoft or third-party applications that you want to run in your environment may not be supported on an SLD. This could have an adverse effect on your environment. Although we'll allow the installation of Exchange 2010 in an SLD, we strongly recommend that you take steps to move your organization out of this configuration.

#### Disjoint Namespaces

In Microsoft Exchange 2010, there are three supported scenarios for deploying Exchange in a domain that has a disjoint namespace. The supported scenarios are as follows:
- Scenario 1: The primary DNS suffix of the domain controller isn't the same as the DNS domain name. Computers that are members of the domain can be either disjoint or not disjoint.
- Scenario 2: A member computer in an Active Directory domain is disjoint even though the domain controller isn't disjoint.
- Scenario 3: The NetBIOS domain name of the domain controller isn't the same as the subdomain of the DNS domain name of that domain controller.

For more information about Exchange 2010 and disjoint namespaces, see [Understanding Disjoint Namespace Scenarios](https://technet.microsoft.com/library/bb676377%28exchg.140%29.aspx).

##### Special Considerations

- In Exchange 2010, you may have to configure the DNS suffix search list to include multiple DNS suffixes if you have a disjoint namespace. For more information, see [Configure the DNS Suffix Search List for a Disjoint Namespace](https://technet.microsoft.com/library/bb847901%28exchg.140%29.aspx).
- Msds-allowedDNSSuffixes must be configured within the Active Directory environment for all namespaces that are used within the forest. For information about how to configure this, see [The computer's primary DNS suffix does not match the FQDN of the domain where it resides](https://technet.microsoft.com/library/aa998420.aspx).

#### Discontiguous (noncontiguous) namespaces

For discontiguous namespaces, DNS must be configured so that Exchange servers can resolve all domain names in the environment. It's also a requirement that msds-allowedDNSSuffixes are configured within the Active Directory environment for all namespaces that are used within the forest.

For information about how to configure this, see [Understanding DNS Client Settings](https://technet.microsoft.com/library/cc754152.aspx).

##### Affected Exchange products include the following:


- [Exchange Server 2013](https://office.microsoft.com/exchange/microsoft-exchange-server-2013-email-for-business-email-server-fx103765014.aspx) 

    For more information about Exchange 2013 system requirements, see [Exchange 2013 System Requirements](https://technet.microsoft.com/library/aa996719%28v=exchg.150%29.aspx).
- [Exchange Server 2010](https://www.microsoft.com/exchange/2010/en/us/overview.aspx) 

    For more information about Exchange 2010 system requirements, see the [Exchange 2010 System Requirements](https://technet.microsoft.com/library/aa996719%28exchg.140%29.aspx) TechNet article.
- [Exchange Server 2007](https://www.microsoft.com/exchange/2010/en/us/exchange-2007-overview.aspx) 

    Microsoft has changed the Setup prerequisite rule for SLDs from an Error to a Warning. This change lets the Service Pack 1 installation continue in SLD environments.

    For known issues and recommendations about Exchange 2007 together with SLD, see the [Exchange Team's Blog Documentation](http://msexchangeteam.com/archive/2008/02/15/448140.aspx).
- [Exchange Server 2003](https://technet.microsoft.com/library/bb123872%28exchg.65%29.aspx) 
- [Exchange 2000 Server](/gp/exch2k) 

## References

[Product Compatibility page on the DNS Namespace Planning Solution Center](/troubleshoot/windows-server/networking/dns-namespace-design)