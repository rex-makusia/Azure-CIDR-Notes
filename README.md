# 🌐 Understanding CIDR Notation in Azure Virtual Networks

> Based on: [Microsoft Premier Developer Blog](https://devblogs.microsoft.com/premier-developer/understanding-cidr-notation-when-designing-azure-virtual-networks-and-subnets/)

## 📚 Table of Contents
- [What is CIDR?](#what-is-cidr)
- [CIDR Breakdown Table](#cidr-breakdown-table)
- [Azure-Specific Considerations](#azure-specific-considerations)
- [Design Tips for Azure VNet/Subnets](#design-tips-for-azure-vnetsubnets)
- [Helpful Tools & Resources](#helpful-tools--resources)

---

## What is CIDR?

**CIDR (Classless Inter-Domain Routing)** is a method of defining IP address ranges.

- **Format:**
`<IP Address>/<Prefix Length>`

Example: `10.0.0.0/16`

- **Network Address:** `10.0.0.0`
- **Prefix Length:** `/16` (means the first 16 bits are the network part)

---

## CIDR Breakdown Table

| CIDR  | Subnet Mask         | Total IPs     | Usable IPs (minus 5 Azure reserved) | Notes                        |
|-------|----------------------|---------------|--------------------------------------|------------------------------|
| /8    | 255.0.0.0            | 16,777,216    | 16,777,211                           | Huge block                   |
| /16   | 255.255.0.0          | 65,536        | 65,531                               | Typical for Azure VNets      |
| /24   | 255.255.255.0        | 256           | 251                                  | Common subnet size           |
| /27   | 255.255.255.224      | 32            | 27                                   | For small workloads/testing  |

📌 **Formula:** `2^(32 - CIDR Prefix)` = Total IPs

---

## Azure-Specific Considerations

When using a subnet in **Azure**, 5 IPs are reserved:

1. Network address
2. First usable IP (Azure gateway)
3. Second usable IP
4. Third usable IP
5. Broadcast address

🧾 **Example:**  
CIDR `/24` ➝ 256 IPs  
Reserved ➝ 5  
Usable ➝ 251

---

## Design Tips for Azure VNet/Subnets

- ✅ **Use /16 or /17 for VNet**: Ample space for multiple subnets.
- ✅ **Subnets of /24 or /27**: Balance between space and simplicity.
- ❌ **Avoid overlapping CIDRs**: Especially across VPN/peering.
- ⚠️ **Plan early**: CIDR changes after deployment are disruptive.

---

## Helpful Tools & Resources

- 🔧 [CIDR to IP Range Calculator](https://www.ipaddressguide.com/cidr)
- 📘 [Azure IP Addressing Docs](https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/)

---
