perfSONAR installer
=========

This perfSONAR role sets up toolkit and testpoint perfSONAR nodes.

Requirements
------------

* Ansile on the jumpbox / bastion host
* perfSONAR role installed

      ansible-galaxy install -f epcjr.perfsonar

Role Variables
--------------

Group Variables, and their default values:

      # Which perfSONAR bundle you would like to install.
      # We currently support:
      #   toolkit
      #   testpoint
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

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
