---
name: Ensure that SSH access is restricted from the internet
slug: azure-1-3-0-networking-2
severity: 3
remediationDescription: >
  Disable direct SSH access to your Azure Virtual Machines from the Internet.
  After direct SSH access from the Internet is disabled, you have other options
  you can use to access these virtual machines for remote management:


  - Point-to-site VPN

  - Site-to-site VPN

  - ExpressRoute


  Default Value


  By default, SSH access from internet is not `enabled`.


  **References:**


  1. [https://docs.microsoft.com/en-us/azure/security/azure-security-network-security-best-practices#disable-rdpssh-access-to-azure-virtual-machines](https://docs.microsoft.com/en-us/azure/security/azure-security-network-security-best-practices#disable-rdpssh-access-to-azure-virtual-machines)

  2. [https://docs.microsoft.com/en-us/azure/security/benchmarks/security-controls-v2-network-security#ns-1-implement-security-for-internal-traffic](https://docs.microsoft.com/en-us/azure/security/benchmarks/security-controls-v2-network-security#ns-1-implement-security-for-internal-traffic)
rules:
  - provider: azure
    comparator: eq
    expectedResult: "[]"
    subjects:
      - SecurityGroup
    query: map-name-security-groups-allowing-public-ssh-slug-sg-public-ssh-query-securitygroups-where-rules_some-direction-inbound-action-allow-and-or-sources_includes-cidr-0-0-0-0-0-sources_includes
---
Disable SSH access on network security groups from the Internet.

**Rationale:**

The potential security problem with using SSH over the Internet is that attackers can use various brute force techniques to gain access to Azure Virtual Machines. Once the attackers gain access, they can use a virtual machine as a launch point for compromising other machines on the Azure Virtual Network or even attack networked devices outside of Azure.
