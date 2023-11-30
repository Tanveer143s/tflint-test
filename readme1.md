# **icardio | Application-Development**
## **1. About**
- All the Infrastructure deployed using Terraform.
- GKE Deployed in developement project.
- Redis Deployed in developement project.
## **2. Cloud Provider & Services**
Icardio has all of its Infrastructure on Google Cloud Provider **(GCP)** in** region **The Dalles (us-west1)**

Following are the GCP resources and services being used in Icardio infra:
## **3. Used of Services & Resources**
### **3.1 GKE-Cluster**
GKE (Google Kubernetes Engine) is a managed service by Google Cloud for deploying, managing, and scaling containerized applications using Kubernetes. It provides an efficient, scalable, and secure environment, abstracting the complexities of Kubernetes infrastructure management, enabling users to focus on developing and running their applications.

Cluster Configuration are as follows:

|**Configurations**|**Values**|
| :-: | :-: |
|project\_id |icardio-dev-project"|
|name|"dev-icardio-gke-cluster"|
|region|"us-west1"|
|network|"dev-vpc"|
|subnetwork|"dev-vpc-subnet-private-1"|
|istio|true|
|filestore\_csi\_driver |true|
|http\_load\_balancing |true|
|horizontal\_pod\_autoscaling|true|
|create\_service\_account|true|
### **3.2 GKE-Node-Pools**
Node pools in GKE are groups of nodes with similar configurations within a Kubernetes cluster. They allow customization for different workloads, support scaling, and enable better resource management by segregating nodes based on specific needs within the same cluster.

There are three (3) types of node-pools added are as follows:
#### **3.2.1. Critical**

|**Configurations**|**Values**|
| :-: | :-: |
|name|“critical”|
|machine\_type|"g1-small"|
|node\_locations|"us-west1-a"|
|min\_count |1|
|max\_count |1|
|disk\_size\_gb |20|
|disk\_type|"pd-standard"|
|image\_type |"ubuntu\_containerd"|
|enable\_node\_pool\_autoscaling|false|
|create\_service\_account |true|
#### **3.2.2. General**

|**Configurations**|**Values**|
| :-: | :-: |
|name|“general”|
|machine\_type|"g1-small"|
|node\_locations|"us-west1-a"|
|min\_count |1|
|max\_count |5|
|disk\_size\_gb |20|
|disk\_type|"pd-standard"|
|image\_type |"ubuntu\_containerd"|
|enable\_node\_pool\_autoscaling|true|
|create\_service\_account |true|
#### **3.2.3. Gpu**

|**Configurations**|**Values**|
| :-: | :-: |
|name|“gpu”|
|machine\_type|"n1-standard-2"|
|node\_locations|"us-west1-a"|
|min\_count |1|
|max\_count |5|
|disk\_size\_gb |20|
|disk\_type|"pd-standard"|
|image\_type |"COS\_CONTAINERD"|
|accelerator\_type|"nvidia-tesla-t4"|
|gpu\_driver\_version |"LATEST"|
|enable\_node\_pool\_autoscaling|true|
|create\_service\_account |true|
#### **3.2.4. Labels, Metadata, Taints, Tags**
```

  node\_pools\_labels = {

    all = {}

    default-node-pool = {

      default-node-pool = true

    }

  }

  node\_pools\_metadata = {

    all = {}

    default-node-pool = {

      node-pool-metadata-custom-value = "my-node-pool"

    }

  }

  node\_pools\_taints = {

    all = []

    default-node-pool = [

      {

        key    = "default-node-pool"

        value  = true

        effect = "PREFER\_NO\_SCHEDULE"

      },

    ]

  }

  node\_pools\_tags = {

    all = []

    default-node-pool = [

      "default-node-pool",

    ]

  }
  
```  
### **3.3 Redis (dev)**
Redis in GKE: Managed Redis service on Google Kubernetes Engine (GKE) offering scalable, in-memory data storage. It utilizes Kubernetes orchestration for deployment, ensuring resilience, scalability, and integration with Google Cloud services.

|**Configurations**|**Values**|
| :-: | :-: |
|name|"dev-redis"|
|project|"icardio-dev-project"|
|region|"us-west1"|
|location\_id |"us-west1-a"|
|alternative\_location\_id|"us-west1-b"|
|enable\_apis|true|
|auth\_enabled|false|
|transit\_encryption\_mode |"SERVER\_AUTHENTICATION"|
|authorized\_network|"dev-vpc"|
|memory\_size\_gb|1|

At the bottom of Redis configuration required config is,
```
  persistence\_config = {

    persistence\_mode    = "RDB"

    rdb\_snapshot\_period = "TWELVE\_HOURS"

  }
```
![](Aspose.Words.73b3eb1c-f2ea-4b1f-8fb2-de26a346b506.001.png) 
## **4. Reference code link:**
[Deployed Dev-application (GKE) Terraform code](https://github.com/clouddrove/icardio/tree/master/terraform/application/development)
