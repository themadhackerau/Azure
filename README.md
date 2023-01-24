# Azure  
## Azure Hints and Tips


A collection of recommendations to help secure Azure Services and Platforms. These are native tools and services that exist within Azure that you can use immediately, some are Free and some are paid. Some of these tools are quite obvious and common, others not so much, the goal here is to highlight what exists already in the platform that can be used to add further layers or security.


### Identity

#### JIT - Just in Time provisioning. 

Azure JIT for VMs works by manipulating Network Security Groups and Blocking Inbound Access to your VM. When a request for access is granted, JIT will open the appropriate remote access port for the specified period of time and then remove it again. Thereby eliminating the need to have remote access ports always opened or filtered to the internet.

Also works with AWS

https://learn.microsoft.com/en-us/azure/defender-for-cloud/just-in-time-access-overview?tabs=defender-for-container-arch-aks

#### PIM - Privileged Identity Management

Privileged Identity Management provides time-based and approval-based role activation to mitigate the risks of excessive, unnecessary, or misused access permissions on resources that you care about. Rather than provide permanent membership to Privileged Administrator Roles, access can be requested, approved or denied and is time bound and audited.

Requires Premium P2 Licence

https://learn.microsoft.com/en-us/azure/active-directory/privileged-identity-management/pim-configure

#### MFA - Multi Factor Authentication

Goes without saying that MFA should be enabled. Azure provides a version of MFA for FREE, it doesnt have the granuality of Conditional Access Policies but still provides a second factor. For a more fully featured option you will need to have a paid licence, which enables Conditional Policies and a bunch of other great configuration options

https://learn.microsoft.com/en-us/azure/active-directory/authentication/concept-mfa-licensing


### Network

#### Service Endpoints -

Virtual Network (VNet) service endpoint provides secure and direct connectivity to Azure services over an optimized route over the Azure backbone network. For example a Azure VM that needs to talk to Blob Storage, doesn't need to traverse the internet which is the default. A Service Endpoint keeps the traffic within the Azure Backbone Network and allows you to secure access to resources from your VNET.

https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-service-endpoints-overview



#### Private Link and Private Endpoints

Private Link provides secure access to Azure services. Private Link achieves that security by replacing a resource's public endpoint with a private network interface. There are three key points to consider with this new architecture:

The Azure resource becomes, in a sense, a part of your virtual network.
The connection to the resource now uses the Microsoft Azure backbone network instead of the public internet.
You can configure the Azure resource to no longer expose its public IP address, which eliminates that potential security risk.


A private endpoint is a network interface that uses a private IP address from your virtual network. This network interface connects you privately and securely to a service that's powered by Azure Private Link. By enabling a private endpoint, you're bringing the service into your virtual network

https://learn.microsoft.com/en-us/training/modules/introduction-azure-private-link/2-what-is-azure-private-link

#### NSGs - Network Security Groups

Basically a set of rules to Deny or Allow access inbound or outbound to your resources. For each rule, you can specify source and destination, port, and protocol. Azure provides some default rules to Allow Inbound access from the Local VNET, and Load Balancer(s) and a Default Inbound Deny Rule. Outbound Defaults include Outbound access to the Local VNET, Outound to the Internet and Default Deny Outbound Rule.

https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview

#### ASGs - Application Security Groups

Allow you to group virtual machines and define network security policies based on those groups. Without having to maintain explicit IP Addresses in the rules. For example a set of web servers can be grouped together with the same inbound ports, without specifically having to set each IP Address. Combine with NSGs.

![image](https://user-images.githubusercontent.com/107555197/214225833-c7852625-5b64-47b2-a64f-be39d1b6ac40.png)


https://learn.microsoft.com/en-us/azure/virtual-network/application-security-groups


### Perimeter

#### WAF - Web Application Firewall

Azure WAF is primarily designed to protect against the OWASP Top 10 Security Risks. It protects web apps from common attacks like SQL Injection, Cross Site Scripting, HTTP Protocol Violations, Bots and Crawlers. Comes preconfigured with Common Rule Sets

https://azure.microsoft.com/en-us/products/web-application-firewall/

https://learn.microsoft.com/en-us/azure/web-application-firewall/ag/application-gateway-crs-rulegroups-rules?tabs=owasp31&culture=en-us&country=us



#### Bastion - Azure Bastion

Azure Bastion provides remote access to your VMs via HTML5 in your browser over port 443. Which means that you do not have to expose remote access ports like 22 (SSH) and 3389 (RDP) to the internet. Instead these can be locked down to the bastion host only. This can be further strengthened by combining Bastion with JIT and only opening ports to the Bastion when requested.

https://azure.microsoft.com/en-us/products/azure-bastion/


![image](https://user-images.githubusercontent.com/107555197/214223199-b24eccfb-839a-4eed-a5b0-563c855cb0e2.png)


#### Azure Firewall

Azure Firewall comes in 2 SKUs - Standard and Premium. Premium provides TLS Inspection, IDS/IPS, URL Filtering. Azure Firewalls can be managed by Azure Firewall Manager for a single pane of glass management. Backed by Microsoft Threat Intelligence.

https://learn.microsoft.com/en-us/azure/firewall/overview

![image](https://user-images.githubusercontent.com/107555197/214223962-cd32fb7b-3e9f-4e24-a1ff-0fc8acd5f8c6.png)

![image](https://user-images.githubusercontent.com/107555197/214223978-7e0d15e2-c394-4977-8668-9485312e5a48.png)


#### Front Door

Microsoft's CDN, available globally. Supports SPLIT TCP, SSL Offload, DDoS Protection. Compatible with Private Link behind Front Door. Available in different SKUs. 

https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview

#### DDoS

Microsoft provides a default level of DDoS protection, however it does not have alerting or telemetry and has much higher threshholds than most applications could handle. If you are running your IaaS Workloads a better option is to upgrade to the Standard Tier. DDoS backed by Microsoft Security Graph.

https://learn.microsoft.com/en-us/azure/ddos-protection/ddos-faq

### Application Security

#### Key Vault

Key Vault provides secure storage and access to Keys, Secrets and Certificates. Permissions can be governed by Azure Active Directory and RBAC or Access Policies. Key vault can support Hardware Security Modules if required. Data is encrytped in transit via TLS.

https://learn.microsoft.com/en-us/azure/key-vault/general/basic-concepts

#### Storage

Every storage account is encrypted by default, customers can choose a Microsoft Managed Key or Customer Managed Key

Access Policies can be enabled such as Legal Hold or Time Based Hold

Secure Transfer Option - only allows access via HTTPs or SMB 3.0

Integrates with Defender for Cloud

https://learn.microsoft.com/en-us/azure/architecture/framework/services/storage/storage-accounts/security

#### SQL Database Security

Comes with built-in firewall, Deny All by Defulat, Can be configured at Server Level or DB level. There is also an option to allow Azure Resources to have access automatically.

##### Discover & Classification Service - 

Can Scan database Tables for sensitive information and can flag recommendations

![image](https://user-images.githubusercontent.com/107555197/214228117-67fd6d03-b1a9-4f52-86cb-e0a3f86e0f5e.png)

##### Transparent Data Encryption (Encryption at Rest) 

All new databases are encrypted by default

##### Always Encrypted -

 Can be enabled on Database Columns via the SQL Management Studio. Provides Encryption in Transit, as the data can only be decrypted at the client end with the appropriate key.
 
 ##### Dynamic Masking -
 
 Automatically discovers sensitive data within the database and can obfuscate specific patterns like Credit Card numbers.

https://learn.microsoft.com/en-us/azure/azure-sql/database/security-overview?view=azuresql



### Monitoring

#### Azure Monitor

Azure Monitor is all about Availability and Monitoring, by collecting Metrics and Logs from your environment. You can build upon Monitor with visualitions and dashboards, integrating with Power BI for even more customisation.

![image](https://user-images.githubusercontent.com/107555197/214226169-67b28a3d-58bb-43c3-baae-579a8abc8830.png)



#### Defender for Cloud

Defender for Cloud is free and works for any PaaS, Data and Network Services within Azure. 
Defender continually Asseses your environment and provides hardening guidance and visibility into your environment.

Can also protect workloads on other cloud like AWS.

Microsoft Documentation - https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-cloud-introduction

![image](https://user-images.githubusercontent.com/107555197/214216574-a801cc74-ad5d-4c48-9582-962ad6051a95.png)

#### Sentinel

Azure Sentinel is Microsoft's Cloud Native SIEM and SOAR Platform. Backed by Microsoft Threat Intelligence. Uses KQL for building queries.

https://learn.microsoft.com/en-us/azure/sentinel/overview


