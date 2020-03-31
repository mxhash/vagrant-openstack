# Vagrant for Openstack and Terraform

This is a Ubuntu Bionic machine to use OpenStack and Terraform with ease.

## QuickStart

Create a file (or alter the existing) ```/vagrant/config/openstack.local.sh```
one with at least the following variables:

```bash
export OS_AUTH_URL=https://identity.mycloud.foo:5000/v3/
export OS_PROJECT_NAME="NAME-OF-PROJECT"
export OS_USERNAME="USERNAME"
export OS_PASSWORD="PASSWORD"
```

After you logged in, the OpenStack and Provider for Terraform are configured.

## Directory Layout

```/vagrant/config```

* Provisioning and configuration files are in here. You can create local config
  files which not affected by git and the provisioner:

```/vagrant/config/openstack.local.sh```

* OpenStack Environment Variables to connect to the cloud
* OS_* vars

```/vagrant/config/terraform.local.sh```

* Terraform Environment
* Terraform OpenStack Provider Environment is automatically set from OpenStack
  client configuration

```/vagrant/log```

* Logging is set to trace and TF logs into this dir

```/vagrant/work```

* You can have your git projects here or just simple scripts and tf projects

## How env vars are build

* Include /etc/profile.d/Z80-openstack.profile.sh
  * Default empty vars are set
  * Include /vagrant/config/openstack.local.sh
  * Sanitize OpenStack env vars
* Include /etc/profile.d/Z81-terraform.profile.sh
  * Set default vars
  * Set OpenStack provider env vars from OS_* vars 
  * Include /vagrant/config/terraform.local.sh