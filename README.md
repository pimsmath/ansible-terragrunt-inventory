ansible-terragrunt-inventory
===========================

A dynamic inventory script for Ansible and Terragrunt. This is a minor
modification of
[ansible-terraform-inventory](https://github.com/jtopjian/ansible-terraform-inventory)
to use terragrunt in place of terraform.

Quickstart
----------

To use this inventory script, you must first create Terraform resources
using the [terraform-provider-ansible](https://github.com/nbering/terraform-provider-ansible)
plugin:

```hcl
resource "ansible_host" "example" {
  inventory_hostname = "example.com"
  groups = ["web"]
  vars {
    ansible_user = "admin"
  }
}

resource "ansible_group" "web" {
  inventory_group_name = "web"
  children = ["foo", "bar", "baz"]
  vars {
    foo = "bar"
    bar = 2
  }
}
```

Next, use this script as your Ansible dynamic inventory script.

Set the TF_STATE environment variable to the directory which would
contain the terraform.tfstate if the state was held locally.

Installation
------------

Download the latest [release](https://github.com/pimsmath/ansible-terragrunt-inventory/releases).

Building From Source
--------------------

```shell
$ go get github.com/pimsmath/ansible-terragrunt-inventory
$ go build -o $GOPATH/bin/terraform-inventory
$ ln -s $GOPATH/bin/terraform-inventory /path/to/ansible/hosts
```
