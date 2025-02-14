---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "Provider: Pritunl"
subcategory: ""
description: |- 
  Terraform provider for interacting with Pritunl API.
---

# Pritunl Provider

## Example Usage

```terraform
terraform {
  required_providers {
    pritunl = {
      version = "~> 0.0.1"
      source  = "disc/pritunl"
    }
  }
}

provider "pritunl" {
  url      = "https://vpn.server.com"
  token    = "api-token"
  secret   = "api-secret-key"
  insecure = false
}

resource "pritunl_organization" "developers" {
  name = "Developers"
}

resource "pritunl_organization" "admins" {
  name = "Admins"
}

resource "pritunl_user" "test" {
  name            = "test-user"
  organization_id = pritunl_organization.developers.id
  email           = "test@test.com"
  groups = [
    "admins",
  ]
}

resource "pritunl_server" "test" {
  name = "test"

  organization_ids = [
    pritunl_organization.developers.id,
    pritunl_organization.admins.id,
  ]

  route {
    network = "10.0.0.0/24"
    comment = "Private network #1"
    nat     = true
  }

  route {
    network = "10.2.0.0/24"
    comment = "Private network #2"
    nat     = false
  }
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Optional

- **insecure** (Boolean)
- **secret** (String)
- **token** (String)
- **url** (String)
