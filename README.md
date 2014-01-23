Ansible IPython Deployment Role
===============================

The [dareko.ipython](https://galaxy.ansibleworks.com/list#/roles/250) role deploys the IPython software on a target host.

The IPython notebook users and groups are created by the role if they don't exist.

GitHub project page: [ansible-ipython](https://github.com/dareko/ansible-ipython).

Requirements
------------

This role requires Ansible 1.4 or higher.
Platform requirements are listed in the Supported Platforms section of the role details.
The rhel-epel yum repository must be enabled on the server.

Role Variables
--------------

The variables that can be passed to this role with default values are as follows.

    # ipython notebooks configuration
    # provide a list of { user, group, port, profile, sha1_password, notebook_dir } items
    # sha1_password can be empty or generated via:
    #     python -c 'from IPython.lib import passwd; print passwd("<password>")'
    ipython_notebooks:
    - user:
      group:
      port:
      profile:
      sha1_password:
      notebook_dir:
    
    # list of dependencies installed via yum
    ipython_dependencies:
    - python-devel
    - python-matplotlib
    
    # list of pip packages
    ipython_pip_packages:
    - pyzmq
    - tornado
    - jinja2
    - pygments
    - pandas
    - pypandoc
    - ipython
    
    proxy_env:
      http_proxy:
      https_proxy:

Example
-------

1. Add a group to the `hosts` inventory file

        [ipython]
        hostname.domainname

2. Add variables to the `group_vars/all` file

        ipython_notebooks:
        - user: user_name
          group: group_name
          port: 8888
          profile: user_name
          sha1_password:
          notebook_dir: /home/user_name/notebooks
        
        proxy_env:
          http_proxy: http://proxy.domain.com:8080
          https_proxy: http://proxy.domain.com:8080

3. Add role to the `site.yml` file

        - hosts: ipython
          sudo: true
          roles:
          - { role: dareko.ipython }

4. Run the `site.yml` playbook

        ansible-playbook -i hosts site.yml

Dependencies
------------

None

License
-------

[MIT License](http://choosealicense.com/licenses/mit/)

Author Information
------------------

[Dariusz Owczarek](https://galaxy.ansibleworks.com/list#/users/1102)
