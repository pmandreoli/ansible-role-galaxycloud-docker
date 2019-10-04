galaxycloud_docker
=========

This role has been specifically developed to be used in the Laniakea project in order to run specific [Galaxy Docker](https://github.com/bgruening/docker-galaxy-stable) container inside a Centos7 virtual machine, creating Galaxy admin user and mounting specific Cern VM file system.



Requirements
------------

This ansible role supports CentOS 7.

Minimum ansible version: 2.1.2.0

Minimum Galaxy docker version: 18.01

Role Variables
--------------

### Main variables ###
 
``galaxy_instance_description``: set galaxy brand, **default** = "ELIXIR-IT"

``export_dir``: directory that will contain the Galaxy directory, and docker_image directory were the docker images will be stored, **default** ="/export"

``galaxy_flavor``: "\<owner>/\<docker\>:<docker_flag\>\", set the Galaxy Docker container, **default** = "bgruening/galaxy-stable:18.05"

``tool_data_table_conf`` :  default path to tool_data_table_conf.xml file = '/etc/galaxy/tool_data_table_conf.xml' 

### Galaxy admin user creation ###

``GALAXY_ADMIN_PASSWORD``: Galaxy administrator password 

``GALAXY_ADMIN_API_KEY``: Galaxy administrator API KEY 

``GALAXY_ADMIN_EMAIL``: Galaxy administrator email

### Galaxy CVMFS role variable ###

``refdata_cvmfs_repository_name``: name of the cvmfs repository to mount inside the Docker container default = "elixir-italy.covacs.refdata"

``server_url``: "<IP ADDRESS OR URL STRATUM 0 OR STRATUM 1 SERVER>", **default** = "90.147.75.251"

``cvmfs_server_url``: "http://{{ server_url }}/cvmfs/{{ refdata_cvmfs_repository_name }}"

``cvmfs_public_key_path``: path were the cvmfs keys will be downloaded, **default** =  "/etc/cvmfs/keys"

``cvmfs_public_key``: "{{ refdata_cvmfs_repository_name }}.pub"

``proxy_url``: "\<PROXY SERVER OR DIRECT>", **default** = DIRECT

``proxy_port``: 80

``cvmfs_http_proxy``: "http://{{ proxy_url }}:{{ proxy_port }}"

``cvmfs_mountpoint``: mountpoint of the docker for the CVMFS server, **default** = "/cvmfs"

### Role templates ###

``default.local.j3``: config file for CVMFS repository that will be mounted on Docker

``delete_galaxy_user.py.j3``: python script run by the role in order to delete the default admin user

``mygalaxyenv.j3``: env file containing the environment variable needed to configure the galaxy docker


Dependencies
------------

role:  [indigo-dc.docker](https://github.com/indigo-dc/ansible-role-docker) : install docker engine and store the docker images inside the export volume 



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




