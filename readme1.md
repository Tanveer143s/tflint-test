# **icardio | Resource Hierarchy**
The resource hierarchy in Google Cloud Platform (GCP) is structured in a hierarchical manner to organize and manage resources effectively. The hierarchy consists of several levels:

1. **Organization Node:** This is the top-level entity representing an organization in GCP. It acts as the root node of the resource hierarchy and is associated with a domain. It can contain folders and projects.
1. **Folders:** Folders are used to group and organize projects within an organization. They allow for logical grouping of projects based on different criteria such as teams, departments, environments, or applications. Folders inherit policies from the organization node and can contain projects and other folders.
1. **Projects:** Projects are fundamental to GCP and serve as containers for resources. They provide boundaries for billing, permissions, and resource management. All GCP resources like virtual machines, databases, storage, etc., belong to a project. Projects inherit policies and permissions from the parent folder or organization.
1. **Resources:** Within each project, various GCP resources such as Compute Engine instances, Cloud Storage buckets, databases, networking components (VPCs, subnets, load balancers), machine learning models, and more are created and managed.

This hierarchical structure allows for effective management, governance, and resource organization within an organization, providing flexibility in controlling access, setting policies, and managing resources across different levels of the hierarchy.
## **Deployed Resource Hierarchy:**
(easy-to-understand resource hierarchy structure )

![](Aspose.Words.958e3c43-77a4-4209-af0f-00870783f196.001.png) 
