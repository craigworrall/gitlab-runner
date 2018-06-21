# VirtualBox for GitLab Runner

Contains a Vagrant file and Ansible playbook to create and provision a vagrant.

Currently the Vagrant file launches a ubuntu/trusty VirtualBox machine. In future, AWS EC2 support
may be addded.

The Ansible playbook downloads, installs and configures the software required on the machine, including:

* GitLab runner software (see GitLab.com for background information).
* Docker

The Runner can thus execute jobs via shell or Docker. In future, additional software may be installed, providing the Runner with additional
execution environment options.

## Configuration

Your GitLab runner token should be configured in the ```default/main.yml``` file. 
