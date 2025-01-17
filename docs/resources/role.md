---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "auth0_role Resource - terraform-provider-auth0"
subcategory: ""
description: |-
  With this resource, you can created and manage collections of permissions that can be assigned to users, which are otherwise known as roles. Permissions (scopes) are created on auth0resourceserver, then associated with roles and optionally, users using this resource
---

# auth0_role (Resource)

With this resource, you can created and manage collections of permissions that can be assigned to users, which are otherwise known as roles. Permissions (scopes) are created on auth0_resource_server, then associated with roles and optionally, users using this resource

## Example Usage

```terraform
resource "auth0_resource_server" "my_resource_server" {
  name                                            = "My Resource Server (Managed by Terraform)"
  identifier                                      = "my-resource-server-identifier"
  signing_alg                                     = "RS256"
  token_lifetime                                  = 86400
  skip_consent_for_verifiable_first_party_clients = true

  enforce_policies = true

  scopes {
    value       = "read:something"
    description = "read something"
  }
}

resource "auth0_user" "my_user" {
  connection_name = "Username-Password-Authentication"
  user_id         = "auth0|1234567890"
  email           = "test@test.com"
  password        = "passpass$12$12"
  nickname        = "testnick"
  username        = "testnick"
  roles           = [auth0_role.my_role.id]
}

resource "auth0_role" "my_role" {
  name        = "My Role - (Managed by Terraform)"
  description = "Role Description..."

  permissions {
    resource_server_identifier = auth0_resource_server.my_resource_server.identifier
    name                       = "read:something"
  }
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- **name** (String) Name for this role

### Optional

- **description** (String) Role's description
- **id** (String) The ID of this resource.
- **permissions** (Block Set) Configuration settings for permissions (scopes) attached to the role (see [below for nested schema](#nestedblock--permissions))

<a id="nestedblock--permissions"></a>
### Nested Schema for `permissions`

Required:

- **name** (String) Name of the permission (scope)
- **resource_server_identifier** (String) Unique identifier for the resource server


