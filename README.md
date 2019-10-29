indigo-dc.galaxycloud_docker
============================

This role has been developed to be used in the Laniakea project in order to run the official [Galaxy Docker](https://github.com/bgruening/docker-galaxy-stable) containers and its flavours on a Centos7 (or Ubuntu 16.04) Virtual Machine, creating Galaxy administrator user and mounting specific CernVM file system.

Galaxy customization
--------------------

- User administrator creation
- Galaxy brand customization
- Anonymous login disabled
- Allow user creation
- Allow user impersonation
- CVMFS customization (default: data.galaxyproject.org)

Requirements
------------

This ansible role supports CentOS 7 and Ubuntu 16.04 Xenial.

Minimum ansible version: 2.1.2.0

Role Variables
--------------

### Main variables ###
 
``galaxy_instance_description``: set galaxy brand, **default** = "ELIXIR-IT"

``export_dir``: directory hosting Galaxy database files and docker images, **default** ="/export"

``galaxy_flavor``: "\<owner>/\<docker\>:<docker_flag\>\", set the Galaxy Docker container, **default** = "bgruening/galaxy-stable:18.05"

``tool_data_table_conf``: default path to tool_data_table_conf.xml file = '/etc/galaxy/tool_data_table_conf.xml' 

### Galaxy admin user creation ###

``GALAXY_ADMIN_PASSWORD``: Galaxy administrator password.

``GALAXY_ADMIN_API_KEY``: Galaxy administrator API KEY.

``GALAXY_ADMIN_EMAIL``: Galaxy administrator email.

### Galaxy CVMFS role variable ###

``refdata_cvmfs_repository_name``: name of the CVMFS repository to mount on the Docker container, **default** = "elixir-italy.covacs.refdata"

``server_url``: IP address or URL of the STRATUM 0 or STRATUM 1 server, **default** = "90.147.75.251"

``cvmfs_server_url``: "http://{{ server_url }}/cvmfs/{{ refdata_cvmfs_repository_name }}"

``cvmfs_public_key_path``: url of the key to download, **default** =  "/etc/cvmfs/keys"

``cvmfs_public_key``: "{{ refdata_cvmfs_repository_name }}.pub"

``proxy_url``: Proxy server or DIRECT, **default** = DIRECT

``proxy_port``: 80

``cvmfs_http_proxy``: "http://{{ proxy_url }}:{{ proxy_port }}"

``cvmfs_mountpoint``: Docker mountpoint for the CVMFS server, **default** = "/cvmfs"

### Role templates ###

``default.local.j2``: config file for CVMFS repository that will be mounted on the Galaxy Docker.

``mygalaxyenv.j2``: env file with the environment variables needed to configure the Galaxy Docker.


Dependencies
------------

[indigo-dc.docker](https://github.com/indigo-dc/ansible-role-docker) : install Docker engine and store the docker images inside the external volume (/export).

Example Playbook
----------------

    - name: minimum playbook
      hosts: localhost
      roles:
        - { role: galaxycloud_docker }
      vars:
        GALAXY_ADMIN_EMAIL: "<your@email>"



License
-------

Apache Licence v2

http://www.apache.org/licenses/LICENSE-2.0


Reference
---------
Galaxy docker: https://github.com/bgruening/docker-galaxy-stable

Laniakea project documentation: https://laniakea.readthedocs.io/en/latest/

Official cvmfs documentation: http://cvmfs.readthedocs.io/en/stable/cpt-repo.html
