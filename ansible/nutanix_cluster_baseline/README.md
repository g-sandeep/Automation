Role Name
=========

This ensures Prism is configured to your desired state.

Requirements
------------

Requires a local cluster admin account on each prism instance to make any changes and port 9440 open through any firewalls.

Role Variables
--------------

This role makes use of the defaults/main.yml to house almost all configurations.
This role was developed with the following inventory format in use to allow for flexability when vars for different scenarios might conflict

/vars
	/Location1
		main.yml #holds specific information for location1
		pc.yml #holds Prism Central specific data
		pe.yml #holds Prism Element specific data
	/Location2
		main.yml
		pc.yml
		pe.yml
	/inventory
		clustername.yml
	/purpose
		vdi.yml #information for VDI clusters
		vsi.yml #information for server virt clusters
	creds.yml
	main.yml


Dependencies
------------

No dependencies on other roles or ansible functions

Example Playbook
----------------

ansible-playbook configure_cluster -e cluster_name="clustername"

---
- hosts: localhost
  tasks:
    - name: configure cluster to desired state
      include_role:
        name: nutanix_cluster_baseline
        tasks_from: configure_cluster/main.yml


Can also use the maintenance tasks to remove proxies or alert settings

---
- hosts: localhost
  tasks:
    - name: configure cluster
      include_role:
        name: nutanix
        tasks_from: maintenance_tasks/remove_proxy.yml

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).