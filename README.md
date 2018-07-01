# GitLab Runner Vagrant

Contains a Vagrant file and Ansible playbook to create and provision a vagrant.

Currently the Vagrant file launches a ubuntu/trusty VirtualBox machine. In future, AWS EC2 support
may be added.

The Ansible playbook downloads, installs and configures the software required on the machine, including:

* GitLab runner software (see GitLab.com for background information).
* Docker

The Runner can thus execute jobs via shell or Docker. By default, the runner is configured to use Docker, employing
the ```alpine:latest``` image if none is specified in your ```.gitlab-ci.yml``` file.

## Configuration

Your GitLab runner token should be configured in the ```default/main.yml``` file:

```
# GitLab registration token
gitlab_runner_registration_token: '...'
```

## Runner Creation

Execute:

```
% vagrant up
```
