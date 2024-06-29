# Ansible role: labocbz.install_glances

![Licence Status](https://img.shields.io/badge/licence-MIT-brightgreen)
![CI Status](https://img.shields.io/badge/CI-success-brightgreen)
![Testing Method](https://img.shields.io/badge/Testing%20Method-Ansible%20Molecule-blueviolet)
![Testing Driver](https://img.shields.io/badge/Testing%20Driver-docker-blueviolet)
![Language Status](https://img.shields.io/badge/language-Ansible-red)
![Compagny](https://img.shields.io/badge/Compagny-Labo--CBZ-blue)
![Author](https://img.shields.io/badge/Author-Lord%20Robin%20Cbz-blue)

## Description

![Tag: Ansible](https://img.shields.io/badge/Tech-Ansible-orange)
![Tag: Debian](https://img.shields.io/badge/Tech-Debian-orange)
![Tag: Python3](https://img.shields.io/badge/Tech-Python3-orange)
![Tag: Python3-jmespath](https://img.shields.io/badge/Tech-Python3--jmespath-orange)
![Tag: Python3-pip](https://img.shields.io/badge/Tech-Python3--pip-orange)
![Tag: Bottle](https://img.shields.io/badge/Tech-Bottle-orange)
![Tag: Glances](https://img.shields.io/badge/Tech-Glances-orange)

An Ansible role to install Glance configure it as service.

The Ansible role installs Glances, a system monitoring tool, on the target system. The role configures Glances to run as a web server by creating a service file. However, the role does not automate the complex procedure of securing the web interface with login credentials.

Upon deployment, Glances provides real-time monitoring of system resources and performance, enhancing administrators' visibility into the system's health. The role allows administrators to customize the refresh time for Glances' web interface, setting the frequency at which the data is updated to the desired value (e.g., 5 seconds).

One key aspect to note is that the role sets the port for Glances' web server to listen on, ensuring the availability of the monitoring interface on the specified port (e.g., 61208).

However, the procedure to secure the web interface with login credentials is not automated within the role. Administrators must manually implement the complex process of setting up authentication and password protection for Glances' web interface to enhance security.

By deploying Glances with this role, administrators can efficiently set up a powerful system monitoring solution with the flexibility to customize the web interface's refresh time and port. While the role establishes the foundation for running Glances as a web server, securing the web interface with login credentials requires additional manual steps.

In summary, the Glances role simplifies the installation and configuration of the system monitoring tool as a web server. It offers customization options for refresh time and port configuration. However, administrators should be aware of the manual steps involved in securing the web interface with login credentials for enhanced security. The role provides an efficient solution for real-time system monitoring, contributing to better system management and performance analysis.

## Folder structure

By default Ansible will look in each directory within a role for a main.yml file for relevant content (also man.yml and main):

```PYTHON
.
├── README.md  # Contains an overview of the role and its purpose.
├── defaults
│   ├── main.yml  # Contains default variables for the role that can be overridden by users.
│   └── README.md  # Contains documentation for the default variables.
├── files
│   └── README.md  # Contains documentation for the files in the directory.
├── handlers
│   ├── main.yml  # Contains handlers that can be called by tasks within the role.
│   └── README.md  # Contains documentation for the handlers.
├── meta
│   ├── main.yml  # Contains metadata about the role, including dependencies and supported platforms.
│   └── README.md  # Contains documentation for the role metadata.
├── tasks
│   ├── main.yml  # Contains tasks to be executed by the role on the managed nodes.
│   └── README.md  # Contains documentation for the tasks.
├── templates
│   └── README.md  # Contains documentation for the templates.
└── vars
    ├── main.yml  # Contains variables that are specific to the role and are not meant to be overridden.
    └── README.md  # Contains documentation for the role variables.
```

## Tests and simulations

### Basics

You have to run multiples tests. *tests with an # are mandatory*

```MARKDOWN
# lint
# syntax
# converge
# idempotence
# verify
side_effect
```

Executing theses test in this order is called a "scenario" and Molecule can handle them.

Molecule use Ansible and pre configured playbook to create containers, prepare them, converge (run the role) and verify its execution.
You can manage multiples scenario with multiples tests in order to get a 100% code coverage.

This role contains a ./tests folder. In this folder you can use the inventory or the tower folder to create a simualtion of a real inventory and a real AWX / Tower job execution.

### Command reminder

```SHELL
# Check your YAML syntax
yamllint -c ./.yamllint .

# Check your Ansible syntax and code security
ansible-lint --config=./.ansible-lint .

# Execute and test your role
molecule create
molecule list
molecule converge
molecule verify
molecule destroy

# Execute all previous task in one single command
molecule test
```

## Installation

To install this role, just copy/import this role or raw file into your fresh playbook repository or call it with the "include_role/import_role" module.

## Usage

### Vars

Some vars a required to run this role:

```YAML
---
install_glances__refresh_time: 5
install_glances__port: 61208

```

The best way is to modify these vars by copy the ./default/main.yml file into the ./vars and edit with your personnals requirements.

You can set vars in the template model in Ansible AWX / Tower or just surchage them during the playbook call.

In order to surchage vars, you have multiples possibilities but for mains cases you have to put vars in your inventory and/or on your AWX / Tower interface.

```YAML
# From inventory
---

inv_install_glances__refresh_time: 5
inv_install_glances__port: 61208

```

```YAML
# From AWX / Tower
---

```

### Run

To run this role, you can copy the molecule/default/converge.yml playbook and add it into your playbook:

```YAML
- name: "Include labocbz.install_glances"
    tags:
    - "labocbz.install_glances"
    vars:
    install_glances__refresh_time: "{{ inv_install_glances__refresh_time }}"
    install_glances__port: "{{ inv_install_glances__port }}"
    ansible.builtin.include_role:
    name: "labocbz.install_glances"
```

## Architectural Decisions Records

Here you can put your change to keep a trace of your work and decisions.

### 2023-04-27: First Init

* First init of this role with the bootstrap_role playbook by Lord Robin Crombez

### 2023-10-06: New CICD, new Images

* New CI/CD scenario name
* Molecule now use remote Docker image by Lord Robin Crombez
* Molecule now use custom Docker image in CI/CD by env vars
* New CICD with needs and optimization

### 2024-02-22: New CICD and fixes

* Added support for Ubuntu 22
* Added support for Debian 11/22
* Edited vars for linting (role name and __)
* Added generic support for Docker dind (can add used for obscures reasons ... user in use)
* Fix idempotency
* Added informations for UID and GID for user/groups
* Added support for user password creation (on_create)
* New CI, need work on tag and releases
* CI use now Sonarqube

### 2024-05-19: New CI

* Added Markdown lint to the CICD
* Rework all Docker images
* Change CICD vars convention
* New workers
* Removed all automation based on branch

## Authors

* Lord Robin Crombez

## Sources

* [Ansible role documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)
