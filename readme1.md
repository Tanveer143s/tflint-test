# **icardio | Projects & Folders**
## **1. About**
- All the Infrastructure deployed using Terraform.
- Folders & Projects Deployed using Terraform

Certainly! In Google Cloud Platform (GCP), folders and projects are organizational constructs that help manage resources effectively:
## **2. Cloud Provider & Services**
Icardio has all of its Infrastructure on Google Cloud Provider **(GCP)** in** region **The Dalles (us-west1)**

Following are the GCP resources and services being used in Icardio infra:
## **3. Used of Services & Resources**
Used organization\_id & billing account for creating folder’s & project’s.

|**Configurations**|**Values**|
| :-: | :-: |
|org\_id|"386725771750"|
|billing\_account|"01DCE1-86986D-06C4CF"|
### **3.1 Folders**
1. **Folders:** Folders are used to group projects hierarchically within an organization. They help organize and manage access control and policies at scale by creating a hierarchy that reflects the organization's structure. Folders inherit policies set at the organization level, allowing administrators to manage permissions, policies, and resources across multiple projects within a logical grouping.

```
module "dev" {

   source  = "terraform-google-modules/folders/google"

   version = "4.0.1"

   parent = "organizations/${var.org\_id}"

   names = [

     "development"

   ]

}


module "prod" {

   source  = "terraform-google-modules/folders/google"

   version = "4.0.1"

   parent = "organizations/${var.org\_id}"

   names = [

     "production"

  ]

}

module "shared" {

   source  = "terraform-google-modules/folders/google"

   version = "4.0.1"

   parent = "organizations/${var.org\_id}"

   names = [

     "shared"

   ]

}

```

- There will be Three Folders created 
  - development
  - production
  - shared
### **3.2 Projects**
**Projects:** Projects are the foundational unit in GCP. They act as containers for resources like virtual machines, storage, databases, and more. They provide isolation, billing boundaries, and IAM (Identity and Access Management) settings. Each GCP resource belongs to a project, and projects can be used to organize and govern resources based on different teams, departments, or applications.
### **3.2.1 Project dev:**

|**Configurations**|**Values**|
| :-: | :-: |
|name|"icardio-dev-project"|
|org\_id |"386725771750"|
|folder\_id |module.dev.id|
|project\_id |"icardio-dev-project"|
|billing\_account|"01DCE1-86986D-06C4CF"|
|activate\_apis |“true”|
|enable\_apis|var.enable\_apis|
### **3.2.2 Project-prod:**

|**Configurations**|**Values**|
| :-: | :-: |
|name|"icardio-prod-project"|
|org\_id |"386725771750"|
|folder\_id |module.prod.id|
|project\_id |"icardio-prod-project"|
|billing\_account|"01DCE1-86986D-06C4CF"|
|activate\_apis |“true”|
|enable\_apis|enable\_apis|
### **3.2.3 Project-shared:**

|**Configurations**|**Values**|
| :-: | :-: |
|name|"icardio-shared-project"|
|org\_id |"386725771750"|
|folder\_id |module.shared.id|
|project\_id |"icardio-shared-project"|
|billing\_account|"01DCE1-86986D-06C4CF"|
|activate\_apis |“true”|
|enable\_apis|enable\_apis|
### **3.3 Api’s List**
```
variable "activate\_apis" {

  type = list(string)

  default = [

    "compute.googleapis.com"

    "iam.googleapis.com"

    "container.googleapis.com"

    "dns.googleapis.com"

    "servicenetworking.googleapis.com"

    "iamcredentials.googleapis.com"

    "logging.googleapis.com"

    "monitoring.googleapis.com"

    "networkconnectivity.googleapis.com"

    "gkeconnect.googleapis.com"

  ]

}
```
## **4. Reference code link:**
[Deployed Folder/Projects Terraform code](https://github.com/clouddrove/icardio/blob/master/terraform/landing-zone/projects.tf)
