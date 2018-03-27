# rhs-connect-host

Is a playbook to migrate an existing RHEL machine that's connected to the customer portal, to Red Hat Satellite 6.

It will check the following before migrating a machine:
  - Machine is RHEL
  - hostname is not localhost.localdomain
  - Ansible can authenticate to Red Hat
  - Ansible can authenticate to Satellite
  - Machine is connected to Red Hat
  - Consumes content from Red Hat
  - Possess a Red Hat license
  - That all enabled repos are present on Satellite* **
  - The hostname doesn't already exist in Satellite
  - Check machine can reach all required Satellite ports

Before migrating it will backup to the machine:
  - System identity
  - Licenses consumed
  - Repos enabled and disabled
  - Configuration

When migrating it will:
  - Remove the machine from Red Hat
  - Install the Katello CA rpm
  - Register the machine with an activation key
  - Enable satellite-tools repo, and install katello-agent
  - Re-enable the repos that were enabled before migrating

You'll need jq installed the machine you're running the playbook from.

*Additionally you'll need your RHS API to support the listing of all [repo-ids] on the system.
** Red Hat say the required patch will be present in Satellite 6.3.1

https://github.com/Katello/katello/commit/ee0fb7f14a04484afdbe91291d4e45adac114da1

Configure the following variables:
```
prechecks_only: true
rhs: rhs.yourdomain.com
api_auth: "username:password"
org: "YOUR_ORG"
rhsm_user: "username"
rhsm_pass: "password"
rhs_port_timeout: 5
rhs_ports:
       - 80
       - 443
       - 5647
activation_key:
   RedHat6: "RHEL6-VM"
   RedHat7: "RHEL7-VM"
conflicts:
       - python-qpid-proton
       - qpid-proton-c
```
