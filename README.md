galaxycloud_docker
=========
Run Galaxy Docker container inside a Centos7 virtual machine, create galaxy admin user and mount Cern VM file system inside the container.
This role has been specifically developed to be used in the Laniakea project.


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

### Galaxy admin user creation ###

``GALAXY_ADMIN_PASSWORD``: Galaxy administrator password 

``GALAXY_ADMIN_API_KEY``: Galaxy administrator API KEY 

``GALAXY_ADMIN_EMAIL``: Galaxy administrator email

### Galaxy CVMFS role variable ###

``repository_name``: name of the cvmfs repository to mount inside the Docker container default = "elixir-italy.covacs.refdata"
``server_url``: "<IP ADDRESS OR URL STRATUM 0 OR STRATUM 1 SERVER>", **default** = "90.147.75.251"
``cvmfs_server_url``: "http://{{ server_url }}/cvmfs/{{ repository_name }}"
``cvmfs_public_key_path``: path were the cvmfs keys will be downloaded, **default** =  "/etc/cvmfs/keys"
``cvmfs_public_key``: "{{ repository_name }}.pub"
``proxy_url``: "\<PROXY SERVER OR DIRECT>", **default** = DIRECT
``proxy_port``: 80
``cvmfs_http_proxy``: "http://{{ proxy_url }}:{{ proxy_port }}"
``cvmfs_mountpoint``: mountpoint of the docker for the CVMFS server, **default** = "/cvmfs"


Dependencies
------------

``role: indigo-dc.docker``


Example Playbook
----------------

    - name: minimum playbook
      hosts: localhost
      roles:
        - { role: galaxycloud_docker }


License
-------

Apache Licence v2

http://www.apache.org/licenses/LICENSE-2.0


Reference
---------
Galaxy docker: https://github.com/bgruening/docker-galaxy-stable

Official cvmfs documentation: http://cvmfs.readthedocs.io/en/stable/cpt-repo.html



