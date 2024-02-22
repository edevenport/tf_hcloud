# tf_hcloud

## Description

The `tf_hcloud` module is a work-in-progress sub-module used by the `tf_hetzner_wireguard*` modules. This module will deploy a simple Hetzner server and firewall ready for configuration through user_data.

## Usage

`main.tf`:

```
module "ssh_keygen" {
  source = "github.com/edevenport/tf_ssh_keygen"

  ssh_key_path = var.secrets_path
}

module "infrastructure" {
  source = "github.com/edevenport/tf_hcloud"

  app_name     = var.app_name
  datacenter   = var.datacenter
  hcloud_token = var.hcloud_token
  image        = var.image
  server_name  = var.server_name
  server_type  = var.server_type
  user_data    = RENDERED_USER_DATA

  ssh_private_key = module.ssh_keygen.private_key
  ssh_public_key  = module.ssh_keygen.public_key
}
```

### Hetzner Datacenters

Below is a list of Hetzner datacenter names and locations. The name is assigned to the `datacenter` variable which currently defaults to `hil-dc1`.

name      | location
--------------------------
nbg1-dc3  | Nuremberg
hel1-dc2  | Helsinki
fsn1-dc14 | Falkenstein
ash-dc1   | Ashburn, VA
hil-dc1   | Hillsboro, OR
