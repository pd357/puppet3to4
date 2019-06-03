# puppet3to4
Upgrade puppet clients 3 to 4 within a Red Hat Satellite environment.

References:
https://access.redhat.com/solutions/3375371
https://bugzilla.redhat.com/show_bug.cgi?id=1547951

Requirements:


Configured and usable Ansible environment.
Configured and usable hammer cli environment.
The client systems must be fully registered and subscribed to Satellite.
Access to 'satellite tools 6.3 with puppet 4' repos.
A properly configured puppet4 master running on a capsule/satellite server.
Auto-signing enabled on the puppet master
Inventory file(s) filled only with clients that match the subnet and
environment of the vars in this playbook.
Configured Satellite user account with the minimal required privileges[1]


Playbook does the following:


Defines subnet for the host via hammer command (Hard Requirement).
Stops puppet (v3) service
Upgrades puppet to latest (v4)
Note: Upgrading puppet renames puppet.conf to puppet.conf.rpmsave
Preserves legacy v3 config data and moves to v4 config path
Modifies lines in the puppet v4 config to address default path changes and any
new vars such as environment or puppet master server:
Starts the puppet (v4) service.


Example usage:
ansible-playbook -K puppet3to4.yml

[1] Creating account with minimal permissions:
Example of creating Satellite Role with permissions for this playbook where
the name of the role is "Bootstrap" and the name of the user account is
"svc_bootstrap".  Note that the role still needs to be manually assigned to the
appropriate site and organization.


Via webui create the user named svc_bootstrap assign mandatory fields and any
appropriate locations and organizations.
Finish account permissions with cli commands:


hammer role create --name "Bootstrap"
hammer user add-role --id svc_bootstrap --role Bootstrap
hammer filter create --role "Bootstrap" --permissions view_organizations
hammer filter create --role "Bootstrap" --permissions view_locations
hammer filter create --role "Bootstrap" --permissions view_domains
hammer filter create --role "Bootstrap" --permissions view_subnets
hammer filter create --role "Bootstrap" --permissions view_hostgroups
hammer filter create --role "Bootstrap" --permissions view_hosts
hammer filter create --role "Bootstrap" --permissions view_architectures
hammer filter create --role "Bootstrap" --permissions view_partitiontables
hammer filter create --role "Bootstrap" --permissions view_operatingsystems
hammer filter create --role "Bootstrap" --permissions create_hosts
hammer filter create --role "Bootstrap" --permissions edit_hosts
hammer filter create --role "Bootstrap" --permissions destroy_hosts
hammer filter create --role "Bootstrap" --permissions view_smart_proxies
References:
https://access.redhat.com/solutions/3375371
https://bugzilla.redhat.com/show_bug.cgi?id=1547951

Updated 20190115.  Added hammer cli task that will define subnet for host as
is now a requirement for puppet.  

Requirements:


Configured and usable Ansible environment.
Configured and usable hammer cli environment.
The client systems must be fully registered and subscribed to Satellite.
Access to 'satellite tools 6.3 with puppet 4' repos.
A properly configured puppet4 master running on a capsule/satellite server.
Auto-signing enabled on the puppet master
Inventory file(s) filled only with clients that match the subnet and
environment of the vars in this playbook.
Configured Satellite user account with the minimal required privileges[1]


Playbook does the following:


Defines subnet for the host via hammer command (Hard Requirement).
Stops puppet (v3) service
Upgrades puppet to latest (v4)
Note: Upgrading puppet renames puppet.conf to puppet.conf.rpmsave
Preserves legacy v3 config data and moves to v4 config path
Modifies lines in the puppet v4 config to address default path changes and any
new vars such as environment or puppet master server:
Starts the puppet (v4) service.


Example usage:
ansible-playbook -K puppet3to4.yml

[1] Creating account with minimal permissions:
Example of creating Satellite Role with permissions for this playbook where
the name of the role is "Bootstrap" and the name of the user account is
"svc_bootstrap".  Note that the role still needs to be manually assigned to the
appropriate site and organization.


Via webui create the user named svc_bootstrap assign mandatory fields and any
appropriate locations and organizations.
Finish account permissions with cli commands:


hammer role create --name "Bootstrap"
hammer user add-role --id svc_bootstrap --role Bootstrap
hammer filter create --role "Bootstrap" --permissions view_organizations
hammer filter create --role "Bootstrap" --permissions view_locations
hammer filter create --role "Bootstrap" --permissions view_domains
hammer filter create --role "Bootstrap" --permissions view_subnets
hammer filter create --role "Bootstrap" --permissions view_hostgroups
hammer filter create --role "Bootstrap" --permissions view_hosts
hammer filter create --role "Bootstrap" --permissions view_architectures
hammer filter create --role "Bootstrap" --permissions view_partitiontables
hammer filter create --role "Bootstrap" --permissions view_operatingsystems
hammer filter create --role "Bootstrap" --permissions create_hosts
hammer filter create --role "Bootstrap" --permissions edit_hosts
hammer filter create --role "Bootstrap" --permissions destroy_hosts
hammer filter create --role "Bootstrap" --permissions view_smart_proxies

