# **icardio | Networking - Dev**
## **1. About**
- All the Networking deployed using Terraform.
## **2. Used of Services & Resources**
### **2.1 Dev-Networking**
Google Cloud Platform (GCP) networking provides a flexible and secure infrastructure. It includes a Virtual Private Cloud (VPC) for creating isolated networks, the global backbone for fast connectivity, load balancing for traffic distribution, a VPN for secure connections, firewall and security measures, monitoring tools, and content delivery options for faster data access. Overall, GCP's networking offers scalability, reliability, and strong security features for cloud-based applications.

|**Configurations**|**Values**|
| :-: | :-: |
|network\_name|"dev-vpc"|
|region|"us-west1"|
|project\_id|"icardio-dev-project"|
|routing\_mode|"GLOBAL"|
|<p>subnet\_name (private)</p><p>subnet\_name (public)</p>|<p>"dev-vpc-subnet-private-1"</p><p>"dev-vpc-subnet-public-1"</p>|
|<p>subnet\_ip (private)</p><p>subnet\_ip (public)</p>|<p>"10.20.0.0/24"</p><p>"10.20.1.0/24"</p>|
|subnet\_region |"us-west1"|
|<p>subnet\_private\_access (private)</p><p>subnet\_private\_access (public)</p>|<p>true</p><p>false</p>|
### **2.2 Secondary ranges used in Network are as follows**
It necessary for GKE

secondary\_ranges for pods are as follows:

|**Configurations**|**Values**|
| :-: | :-: |
|range\_name|"gke-dev-icardio-gke-cluster-pods-6849b9c3"|
|ip\_cidr\_range|"10.52.0.0/14"|

secondary\_ranges for services are as follows:

|**Configurations**|**Values**|
| :-: | :-: |
|range\_name|"gke-dev-icardio-gke-cluster-services-6849b9c3"|
|ip\_cidr\_range|"10.56.0.0/20"|
### **2.3 Firewall rules used for networking.**

|**Firewall\_rules**|**Values**|
| :-: | :-: |
|name|"icardio-allow-all"|
|priority|10000|
|allow-protocol|tcp|
|ports|["1-65535"]|
|ranges|<p>"10.20.0.0/24", "10.20.1.0/24",</p><p>"10.10.0.0/24", "10.10.1.0/24"</p>|

We added the shared and development subnetwork IPs to the aforementioned ranges for VPC peering.
## **3. Reference code link:**
[Deployed Dev-networking Terraform code](https://github.com/clouddrove/icardio/tree/master/terraform/networking/development)
