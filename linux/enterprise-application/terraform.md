# Terraform



Example of deploy multiple vms on vsphere

[https://github.com/ewypych/terraform-vsphere-multiple-vm](https://github.com/ewypych/terraform-vsphere-multiple-vm)

{% code-tabs %}
{% code-tabs-item title="main.tf" %}
```text
provider "vsphere" { 
    #vsphere_server = "10.10.10.142"
    #user = "administrator@vsphere.local"
    #password = "Password"
    
    vsphere_server = "${var.vsphere_server}"
    user =  "${var.vsphere_user}"
    password = "${var.vsphere_password}"
    allow_unverified_ssl = true
}



```
{% endcode-tabs-item %}
{% endcode-tabs %}

```text
variable "vsphere_server" {
    description = "vsphere server for live"
    default = "10.84.89.142" 
}

variable "vsphere_user" {
    description = "vsphere server for live"
    default = "administrator@vsphere.local"
}

variable "vsphere_password" {
    description = "vsphere server for live"
    default = "Password"
}


variable "virtul_machine_dns_servers" {
    type = "list"
    default = ["8.8.8.8","8.8.4.4"]
}


```

```text
data "vsphere_datacenter" "dc" {
  name = "VN-Esxi"
}
 
data "vsphere_datastore" "datastore" {
  name          = "VN-LIVE"
  datacenter_id = "${data.vsphere_datacenter.dc.id}"
}
 
data "vsphere_compute_cluster" "cluster" {
  name          = "VN-CM"
  datacenter_id = "${data.vsphere_datacenter.dc.id}"
}
 
data "vsphere_network" "network" {
  name          = "VM Network"
  datacenter_id = "${data.vsphere_datacenter.dc.id}"
}
 
data "vsphere_virtual_machine" "template" {
  name          = "CentOS"
  datacenter_id = "${data.vsphere_datacenter.dc.id}"
}




resource "vsphere_virtual_machine" "vm-web" {
  count = "25" #number of instance
  name             = "centos7-${count.index + 1}"
  resource_pool_id = "${data.vsphere_compute_cluster.cluster.resource_pool_id}"
  datastore_id     = "${data.vsphere_datastore.datastore.id}"
 
  num_cpus = 2
  memory   = 1024
  guest_id = "${data.vsphere_virtual_machine.template.guest_id}"
 
  scsi_type = "${data.vsphere_virtual_machine.template.scsi_type}"
 
  network_interface {
    #network_id   = "${data.vsphere_network.network.id}"
    #adapter_type = "${data.vsphere_virtual_machine.template.network_interface_types[0]}"
    label = "${lookup(var.vmnetlabel, var.vmdomain)}"
    ipv4_address = "10.5.5.${10 + count.index}"
    ipv4_gateway = "10.5.5.1"
    ipv4_prefix_length = "24"
  }
 
  disk {
    label            = "disk0"
    size             = "${data.vsphere_virtual_machine.template.disks.0.size}"
    eagerly_scrub    = "${data.vsphere_virtual_machine.template.disks.0.eagerly_scrub}"
    thin_provisioned = "${data.vsphere_virtual_machine.template.disks.0.thin_provisioned}"
  }
 
  clone {
    template_uuid = "${data.vsphere_virtual_machine.template.id}"
 
    #customize {
    #  linux_options {
    #    host_name = "centos7_test_01"
    #    domain = "test.internal"
    #  }
 
    #  network_interface {
    #    ipv4_address = "10.1.149.29"
    #    ipv4_netmask = 24
    #  }
 
    #  ipv4_gateway = "10.1.149.1"
    #}
  }
}

```

{% code-tabs %}
{% code-tabs-item title="module example" %}
```text
module "web-servers" {
  source = "Terraform-VMWare-Modules/vm/vsphere"
  version           = "0.9.2"
  vmtemp            = "Template_web"
  instances         = 3
  vmname            = "linux"
  vmrp              = "esxi/Resources"  
  vlan              = "Name of the VLAN in vSphere"
  data_disk         = "true"
  data_disk_size_gb = 20
  dc                = "Datacenter"
  ds_cluster        = "Data Store Cluster name"

}
module "db-servers" {
  source = "Terraform-VMWare-Modules/vm/vsphere"
  version           = "0.9.2"
  vmtemp            = "Template_db"
  instances         = 3
  vmname            = "linux"
  vmrp              = "esxi/Resources"  
  vlan              = "Name of the VLAN in vSphere"
  data_disk         = "true"
  data_disk_size_gb = 20
  dc                = "Datacenter"
  ds_cluster        = "Data Store Cluster name"

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

