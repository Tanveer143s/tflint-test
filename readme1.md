# Landing Zone in Google Cloud Platform (GCP)

Landing zones are a crucial aspect in GCP, encompassing the creation of IAM roles, groups, bindings, folders, projects, etc.

## IAM Role Groups and User Permissions

IAM role groups are created and associated with users within the group, assigning specific permissions to those users. Three groups and their associated permissions are outlined:

### Groups

- `admins`
- `developer`
- `read-only`

### Permissions Added for Users

- `owner`
- `editor`
- `read-only`

## Used Services & Resources

### 2.1 IAM Groups & Added Members in Group

```yaml
data "google_organization" "org" {
  organization = "organizations/${var.org_id}"
}

resource "google_cloud_identity_group" "admins" {
  display_name         = "admins"
  initial_group_config = "WITH_INITIAL_OWNER"

  parent = "customers/${data.google_organization.org.directory_customer_id}"

  group_key {
    id = "admins@icardio.ai"
  }

  labels = {
    "cloudidentity.googleapis.com/groups.discussion_forum" = ""
  }
}

resource "google_cloud_identity_group" "developer" {
  display_name         = "developer"
  initial_group_config = "WITH_INITIAL_OWNER"

  parent = "customers/${data.google_organization.org.directory_customer_id}"

  group_key {
    id = "developer@icardio.ai"
  }

  labels = {
    "cloudidentity.googleapis.com/groups.discussion_forum" = ""
  }
}

resource "google_cloud_identity_group" "read-only" {
  display_name         = "read-only"
  initial_group_config = "WITH_INITIAL_OWNER"

  parent = "customers/${data.google_organization.org.directory_customer_id}"

  group_key {
    id = "read-only@icardio.ai"
  }

  labels = {
    "cloudidentity.googleapis.com/groups.discussion_forum" = ""
  }
}

resource "google_cloud_identity_group_membership" "admins_add_member" {
  group = google_cloud_identity_group.admins.id

  preferred_member_key {
    id = "anmol@icardio.ai"
  }
  roles {
    name = "MEMBER"
  }
  roles {
    name = "OWNER"
  }
}

resource "google_cloud_identity_group_membership" "developer_add_member" {
  group = google_cloud_identity_group.developer.id

  preferred_member_key {
    id = "anmol@icardio.ai"
  }
  roles {
    name = "MEMBER"
  }
  roles {
    name = "OWNER"
  }
}

resource "google_cloud_identity_group_membership" "readonly_add_member" {
  group = google_cloud_identity_group.read-only.id

  preferred_member_key {
    id = "anmol@icardio.ai"
  }
  roles {
    name = "MEMBER"
  }
  roles {
    name = "OWNER"
  }
}
```
### Project bind with IAM groups:

```
module "shared-bind" {
  source  = "terraform-google-modules/iam/google//modules/projects_iam"
  version = "~> 7.4"

  projects = [
    module.project-shared.project_id,
  ]
  bindings = {
    "roles/owner" = [
      "group:admins@icardio.ai",
    ],
    "roles/editor" = [
      "group:developer@icardio.ai",
    ]
    "roles/viewer" = [
      "group:read-only@icardio.ai",
    ]
  }
}

module "dev-bind" {
  source  = "terraform-google-modules/iam/google//modules/projects_iam"
  version = "~> 7.4"

  projects = [
    module.project-dev.project_id,
  ]
  bindings = {
    "roles/owner" = [
      "group:admins@icardio.ai",
    ],
    "roles/editor" = [
      "group:developer@icardio.ai",
    ]
    "roles/viewer" = [
      "group:read-only@icardio.ai",
    ]
  }
}

module "prod-bind" {
  source  = "terraform-google-modules/iam/google//modules/projects_iam"
  version = "~> 7.4"

  projects = [
    module.project-prod.project_id,
  ]
  bindings = {
    "roles/owner" = [
      "group:admins@icardio.ai",
    ],
    "roles/editor" = [
      "group:developer@icardio.ai",
    ]
    "roles/viewer" = [
      "group:read-only@icardio.ai",
    ]
  }
}

```

## Reference Link:

![Deployed IAM Terraform code] (https://github.com/clouddrove/icardio/blob/master/terraform/landing-zone/iam.tf)
