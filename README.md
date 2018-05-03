perfSONAR
=========

This perfSONAR role sets up toolkit and testpoint perfSONAR nodes.

Requirements
------------

* Ansible on the jumpbox / bastion host
* perfSONAR role installed

      $ ansible-galaxy install -f epcjr.perfsonar

Role Variables
--------------

Group Variables, and their default values:

      # Which perfSONAR bundle you would like to install.
      # We currently support:
      #   perfsonar-toolkit
      #   perfsonar-testpoint
      #
      # This is a required option.
      #
      perfsonar_bundle: 
      
      # This is a list of local users with ssh keys.  They will be
      # provisioned with user accounts on the perfSONAR nodes, and
      # their ssh keys will be copied over.
      #
      perfsonar_users: []
      
      # This is a list of bastion hosts.  If this list is populated,
      # ssh will be restricted on the perfSONAR nodes to these machines
      # only.
      #
      perfsonar_bastion_hosts: []
      
      # Disable root ssh if true
      #
      perfsonar_disable_root_ssh : false
      
      # A list of nameservers to add to resolv.conf
      #
      perfsonar_nameservers: []
      
      # A list of ntp servers to add to ntpd.conf
      #
      perfsonar_ntpservers: []
      
      # A list of perfSONAR nodes to initially troubleshoot to after install.
      #
      perfsonar_troubleshoot: []


Toolkit Variables.  These manage the toolkit's web user.  They are undeclared by default.

      perfsonar_web_user:
      perfsonar_web_passwd:
  
Testpoint Variables.  These can elect to use optional packages normally included in the toolkit.

      # See more here: http://docs.perfsonar.net/install_centos.html
      #
      
      # NTP more info: http://docs.perfsonar.net/manage_ntp.html
      #
      perfsonar_toolkit_ntp: false
      
      # System Tuning info here: http://docs.perfsonar.net/install_centos.html#step-3-verify-ntp-and-tuning-parameters
      # More here: http://docs.perfsonar.net/manage_tuning.html
      #
      perfsonar_toolkit_configure_sysctl: false
      
      # Security module more info: http://docs.perfsonar.net/install_centos.html#step-4-firewall-and-security-considerations
      # More here: http://docs.perfsonar.net/manage_security.html
      perfsonar_toolkit_security: false
      
      # Autoupdate more info: http://docs.perfsonar.net/manage_update.html
      #
      perfsonar_autoupdate: false
      
      # Service watcher info: http://docs.perfsonar.net/install_centos.html#step-6-service-watcher
      #
      perfsonar_toolkit_service_watcher: false
      
Host Variables, only set on a per-host basis.  They are undeclared by default.

      # Set the hostname of the machine if set
      #
      perfsonar_hostname:
      
      # This is used for multi-interface machines only.
      # Define the interface's name and gateway and it will set up the routes
      # with the perfSONAR multi-interface script.
      #
      # See more here: http://docs.perfsonar.net/manage_dual_xface.html
      #
      perfsonar_interfaces:
        - name:
          ipv4_gateway:
        - name:
          ipv4_gateway:

Dependencies
------------

None.

Example Playbook
----------------

perfsonar_site.yml:

    - hosts: testpoints
      vars_files:
        - vars/perfsonar_vars.yml
      roles:
         - { role: epcjr.perfsonar, perfsonar_bundle: testpoint }

    - hosts: toolkits
      vars_files:
        - vars/perfsonar_vars.yml
      roles:
         - { role: epcjr.perfsonar, perfsonar_bundle: toolkit }

vars/perfsonar_vars.yml:

      # General perfsonar node settings
      perfsonar_users:
        - myuid
      perfsonar_bastion_hosts:
        - bastion.example.com
      perfsonar_disable_root_ssh: true
      # Use Google's public nameservers
      perfsonar_nameservers:
        - 8.8.8.8
        - 8.8.4.4
      # add Google's ntp server
      perfsonar_ntpservers:
        - 216.239.35.0
      # troubleshoot to I2
      perfsonar_troubleshoot:
        - perfsonardev0.internet2.edu
      
      # Variables for Toolkits Only
      perfsonar_web_user: pswebadmin
      # secrets can be encrypted with Ansible vault:
      # ansible-vault encrypt_string 'secret' --ask-vault-pass --name=perfsonar_web_passwd
      perfsonar_web_passwd: secret
      
      #Variables for Testpoints Only
      perfsonar_toolkit_ntp: true
      perfsonar_toolkit_configure_sysctl: true
      perfsonar_toolkit_security: true
      perfsonar_autoupdate: true
      perfsonar_toolkit_service_watcher: true
      
host_vars/example_ps_host

      # Set hostname and configure multiple interfaces
      perfsonar_hostname: example_ps_host
      perfsonar_interfaces:
        - interface_name: em0
          interface_gateway_ipv4: 1.2.3.4
        - interface_name: p0p0
          interface_gateway_ipv4: 5.6.7.8



License
-------

Apache 2.0

Author Information
------------------


