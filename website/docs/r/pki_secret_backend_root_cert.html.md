---
layout: "vault"
page_title: "Vault: vault_pki_secret_backend_root_cert resource"
sidebar_current: "docs-vault-resource-pki-secret-backend-root-cert"
description: |-
  Generate root.
---

# vault\_pki\_secret\_backend\_root\_cert

Generates a new self-signed CA certificate and private keys for the PKI Secret Backend.

~> **Important** All data provided in the resource configuration will be
written in cleartext to state and plan files generated by Terraform, and
will appear in the console output when Terraform runs. Protect these
artifacts accordingly. See
[the main provider documentation](../index.html)
for more details.

## Example Usage

```hcl
resource "vault_pki_secret_backend_root_cert" "test" {
  depends_on = [vault_pki_secret_backend.pki]

  backend = vault_pki_secret_backend.pki.path

  type                 = "internal"
  common_name          = "Root CA"
  ttl                  = "315360000"
  format               = "pem"
  private_key_format   = "der"
  key_type             = "rsa"
  key_bits             = 4096
  exclude_cn_from_sans = true
  ou                   = "My OU"
  organization         = "My organization"
}
```

## Argument Reference

The following arguments are supported:

* `backend` - (Required) The PKI secret backend the resource belongs to.

* `type` - (Required) Type of intermediate to create. Must be either \"exported\" or \"internal\"

* `common_name` - (Required) CN of intermediate to create

* `alt_names` - (Optional) List of alternative names

* `ip_sans` - (Optional) List of alternative IPs

* `uri_sans` - (Optional) List of alternative URIs

* `other_sans` - (Optional) List of other SANs

* `ttl` - (Optional) Time to live

* `format` - (Optional) The format of data

* `private_key_format` - (Optional) The private key format

* `key_type` - (Optional) The desired key type

* `key_bits` - (Optional) The number of bits to use

* `max_path_length` - (Optional) The maximum path length to encode in the generated certificate

* `exclude_cn_from_sans` - (Optional) Flag to exclude CN from SANs

* `permitted_dns_domains` - (Optional) List of domains for which certificates are allowed to be issued

* `ou` - (Optional) The organization unit

* `organization` - (Optional) The organization

* `country` - (Optional) The country

* `locality` - (Optional) The locality

* `province` - (Optional) The province

* `street_address` - (Optional) The street address

* `postal_code` - (Optional) The postal code

## Attributes Reference

In addition to the fields above, the following attributes are exported:

* `certificate` - The certificate

* `issuing_ca` - The issuing CA

* `serial` - The serial
