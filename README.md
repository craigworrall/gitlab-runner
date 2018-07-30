# GitLab Runner

Contains a Vagrant file and Ansible playbook to create and provision a GitLab Runner.

Currently the Vagrant file launches a ubuntu/trusty VirtualBox machine. In future, AWS EC2 support
may be added.

The Ansible playbook downloads, installs and configures the software required on the machine, including:

* GitLab runner software (see GitLab.com for background information).
* Docker

The Runner can thus execute jobs via shell or Docker. By default, the runner is configured to use Docker, employing
the ```alpine:latest``` image if none is specified in your ```.gitlab-ci.yml``` file.

## Ubuntu Versions

Both Trusty and Xenial are supported.

### Xenial

To use Xenial, geerlingguy.docker role must be used. It should be cloned into the same directory that includes ```runner```,
after which the following changes are needed:

```
-- name: Install Docker
-  import_tasks: docker.yml
+#- name: Install Docker
+#  import_tasks: docker.yml
```
and to site.yml:
```
-    - runner
+    - ansible-role-docker
+    - runner
```

## Configuration

Your GitLab runner token should be configured in the ```default/main.yml``` file:

```
# GitLab registration token
gitlab_runner_registration_token: '...'
```

## Vagrant Creation

Execute:

```
% vagrant up
```

## Local Playbook Execution

Change ```site.yml``` as follows:

```
-- hosts: all
+- hosts: localhost
```

Execute:

```
ansible-playbook -K -i inventory.local site.yml 
```

## AWS

The following sections describe steps necessary to deploy onto an EC2 instance.

### Branch

Checkout AWS branch:
```
% git checkout aws
```

### Setup

Ensure Vagrant's AWS provider has been installed and add the dummy box:
```
% vagrant plugin install vagrant-aws
% vagrant box add aws-dummy https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box
```

Set the Security Group name in the vagrant file, or use the default (```vagrant```) group after
ensuring it allows SSH access.

Set the Key Pair name in the vagrant file as appropriate.

## EC2 Vagrant Creation

Execute:
```
% vagrant up --provider=aw
```
