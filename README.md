# rhs-connect-host

Is a playbook to migrate an existing RHEL machine that's connected to the customer portal, to Red Hat Satellite 6.

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
