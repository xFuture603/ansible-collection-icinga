# Icinga Collection for Ansible

This Ansible collection contains:

  1. A [role](roles/icinga_agent) to manage the Installation for your Icinga agents

  2. A [role](roles/icinga_plugins) to deploy your custom check scripts to your Icinga agents
  
  3. A [role](roles/icinga_downtime) to manage downtimes in your Icinga

  3. The [collection](https://github.com/T-Systems-MMS/ansible-collection-icinga-director) to deploy your Icinga master via the Icinga Director module

  4. An extra [collection](https://github.com/T-Systems-MMS/ansible-collection-icinga-business-process) to use the [Business Process module](https://github.com/Icinga/icingaweb2-module-businessprocess)

  5. Ansible playbooks to create various objects in Icinga 2 using the director API

## Requirements

- Ansible version: 2.9.10
- Icinga package repository configured
- Note: for Redhat based Distributions you need to have install epel package repository too

## Installation

If you use an older version, you can install it with Ansible Galaxy:
```
ansible-galaxy collection install t_systems_mms.ansible_collection_icinga
```

Alternatively put the collection into a `requirements.yml` file:
```
---
collections:
  - t_systems_mms.ansible_collection_icinga
```

## Documentation

**icinga_agent role:**

Examples on how to use the role can be found [here](roles/icinga_agent/README.md)

**icinga_plugins role:**

Examples on how to use the role can be found [here](roles/icinga_plugins/README.md)


**icinga_director collection:**

Check out the 'Documentation' part for the modules [here](https://github.com/T-Systems-MMS/ansible-collection-icinga-director#documentation)

**icinga_business_process collection:**

Check out the 'Documentation' part for this collection [here](https://github.com/T-Systems-MMS/ansible-collection-icinga-business-process/blob/master/roles/ansible_icinga_business_process/README.md)

**icinga playbooks:**

| playbook| description
|------------|-----------------------------------------------------------------------
| mms_standard.yml | create a timeperiod and service template to use for other checks
| azure_oauth_token.yml | get azure oauth token to use in other checks
| check_gitlab_scheduler.yml | check gitlab scheduled pipelines
| check_https.yml | check https reachability and certificates
| check_json_azure_restapi_resourcehealth.yml | check state of azure resourcehealth
| check_json_azure_restapi.yml | do a json check against azure restapi (with oauth_token)
| check_json.yml | do a json check
| template_empty_host.yml | create a host template for an empty host

You can use these playbooks in your playbook like this:

```
- name: Import mms standard playbook to create services that other checks depend on
  import-playbook: t_systems_mms.ansible_collection_icinga.mms_standard

- name: Import playbook to create azure oauth token check
  import-playbook: t_systems_mms.ansible_collection_icinga.check_azure_oauth_token

- name: Import playbook to create gitlab_scheduler check
  import-playbook: t_systems_mms.ansible_collection_icinga.check_gitlab_scheduler

- name: Import playbook to create check_https checks
  import-playbook: t_systems_mms.ansible_collection_icinga.check_https

```

Or call them from the command line:
```
ansible-playbook t_systems_mms.ansible_collection_icinga.mms_standard
ansible-playbook t_systems_mms.ansible_collection_icinga.check_azure_oauth_token
ansible-playbook t_systems_mms.ansible_collection_icinga.check_gitlab_scheduler
ansible-playbook t_systems_mms.ansible_collection_icinga.check_https
ansible-playbook t_systems_mms.ansible_collection_icinga.check_json
ansible-playbook t_systems_mms.ansible_collection_icinga.check_json_azure_restapi
ansible-playbook t_systems_mms.ansible_collection_icinga.check_json_azure_restapi_resourcehealth
ansible-playbook t_systems_mms.ansible_collection_icinga.template_empty_host
```

## License

GPLv3

## Author Information

* Christopher Grau
* Daniel Uhlmann
* Contributors from [ansible-collection-icinga-director ](https://github.com/T-Systems-MMS/ansible-collection-icinga-director/graphs/contributors)
* Contributors from [ansible-collection-icinga-business-process](https://github.com/T-Systems-MMS/ansible-collection-icinga-business-process/graphs/contributors)
