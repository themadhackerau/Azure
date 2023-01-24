# Azure  
## Azure Hints and Tips


A collection of recommendations to help secure Azure Services and Platforms. These are native tools and services that exist within Azure that you can use immediately.


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


### Perimeter

WAF

Bastion

Firewall

Front Door


### Monitoring

Azure Monitor


#### Defender for Cloud

Defender for Cloud is free and works for any PaaS, Data and Network Services within Azure. 
Defender continually Asseses your environment and provides hardening guidance and visibility into your environment.

Can also protect workloads on other cloud like AWS.

Microsoft Documentation - https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-cloud-introduction

![image](https://user-images.githubusercontent.com/107555197/214216574-a801cc74-ad5d-4c48-9582-962ad6051a95.png)

Sentinel


