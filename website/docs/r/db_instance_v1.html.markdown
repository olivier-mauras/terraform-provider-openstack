---
layout: "openstack"
page_title: "OpenStack: openstack_db_instance_v1"
sidebar_current: "docs-openstack-resource-db-instance-v1"
description: |-
  Manages a V1 DB instance resource within OpenStack.
---

# openstack\_db\_instance_v1

Manages a V1 DB instance resource within OpenStack.

## Example Usage

### Instance

```hcl
resource "openstack_db_instance_v1" "test" {
  region    = "region-test"
  name      = "test"
  flavor_id = "31792d21-c355-4587-9290-56c1ed0ca376"
  size      = 8

  network {
    uuid = "c0612505-caf2-4fb0-b7cb-56a0240a2b12"
  }

  datastore {
    version = "mysql-5.7"
    type    = "mysql"
  }
}
```

## Argument Reference

The following arguments are supported:

* `region` - (Required) The region in which to create the db instance. Changing this
    creates a new instance.

* `name` - (Required) A unique name for the resource.

* `flavor_id` - (Required) The flavor ID of the desired flavor for the instance.
    Changing this creates new instance.

* `size` - (Required) Specifies the volume size in GB. Changing this creates new instance.

* `datastore` - (Required) An array of database engine type and version. The datastore
    object structure is documented below. Changing this creates a new instance.

* `network` - (Optional) An array of one or more networks to attach to the
    instance. The network object structure is documented below. Changing this
    creates a new instance.

The `datastore` block supports:

* `type` - (Required) Database engine type to be used in new instance. Changing this
    creates a new instance.
* `version` - (Required) Version of database engine type to be used in new instance.
    Changing this creates a new instance.

The `network` block supports:

* `uuid` - (Required unless `port` is provided) The network UUID to
    attach to the instance. Changing this creates a new instance.

* `port` - (Required unless `uuid` is provided) The port UUID of a
    network to attach to the instance. Changing this creates a new instance.

* `fixed_ip_v4` - (Optional) Specifies a fixed IPv4 address to be used on this
    network. Changing this creates a new instance.

* `fixed_ip_v6` - (Optional) Specifies a fixed IPv6 address to be used on this
    network. Changing this creates a new instance.

## Attributes Reference

The following attributes are exported:

* `region` - See Argument Reference above.
* `name` - See Argument Reference above.
* `size` - See Argument Reference above.
* `flavor_id` - See Argument Reference above.
* `datastore/type` - See Argument Reference above.
* `datastore/version` - See Argument Reference above.
* `network/uuid` - See Argument Reference above.
* `network/port` - See Argument Reference above.
* `network/fixed_ip_v4` - The Fixed IPv4 address of the Instance on that
    network.
* `network/fixed_ip_v6` - The Fixed IPv6 address of the Instance on that
    network.
