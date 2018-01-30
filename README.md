# magento2-ansible-vagrant

> Ansible provisioned Ubuntu 16.04 vagrant box for [Magento2](https://github.com/magento/magento2) development.

Definitely not full-featured but useful to bootstrap a dev project.

## Prerequisites

- Vagrant
- VirtualBox

This box uses [Ansible Local Provisioner](https://www.vagrantup.com/docs/provisioning/ansible_local.html).
As a result, Ansible do **not** need to be installed on the host.

## Base box

[geerlingguy/ubuntu1604](https://atlas.hashicorp.com/geerlingguy/boxes/ubuntu1604/)

## Roles

- Dev tools: git, vim, curl, htop
- PHP (7.0 + Composer + Xdebug)
- Nginx
- Redis (for session, full page cache and frontend cache)
- MariaDB 10.0 (dedicated user and database)
- Magento2 (automated project creation if directory is empty, installation and configuration)

## Get started

### 1. Clone this repository

```bash
git clone https://github.com/sawyer-effect/magento2-ansible-vagrant
```

### 2. Configure

Create a dev.yml conf file in ansible/group_vars:

```bash
cd magento2-ansible-vagrant
cp ansible/group_vars/dev.yml.sample ansible/group_vars/dev.yml
```

And configure your environment:

```yaml
magento_account_public_key: YOUR_PUBLIC_KEY_HERE
magento_account_private_key: YOUR_PRIVATE_KEY_HERE
mysql_user: magento2
mysql_password: magento2
mysql_dbname: magento2
magento2_admin_password: ADMIN_PASSWORD
magento2_admin_email: ADMIN_EMAIL
magento2_admin_firstname: ADMIN_NAME
magento2_admin_lastname: ADMIN_LASTNAME
```

How generate public and private keys: http://devdocs.magento.com/guides/v2.0/install-gde/prereq/connect-auth.html

Admin values are the same of your Magento Marketplace Account.

### External project

You can find a statement in Vagrantfile to copy magento folder from another project folder.

If that line is removed, the provisioning will install magento in the VM.


### 4. Up!

```bash
vagrant up
```

### 5. It's ready!

Add this entry in `/etc/hosts`: "192.168.33.10 pinedacovalin.magemojo.io"

You can visit the website in: http://pinedacovalin.magemojo.io
