[![Build Status](https://travis-ci.com/AlexisCangelosi/openvpn.svg?branch=master)(https://travis-ci.com/AlexisCangelosi/openvpn)
<br />
[![Build Status](https://travis-ci.org/klugjo/hexo-autolinker.svg?branch=master)](https://travis-ci.org/klugjo/hexo-autolinker)
<br />

Role Name
=========

Install OpenVPN, server and client configuration

Role Variables
--------------

	### Easy-RSA vars
	openvpn_easyrsa_keysize: 2048
	openvpn_easyrsa_ca_expire: 3650
	openvpn_easyrsa_key_expire: 3650
	
	openvpn_easyrsa_country: "US"
	openvpn_easyrsa_province: "CA"
	openvpn_easyrsa_city: "SanFrancisco"
	openvpn_easyrsa_org: "Fort-Funston"
	openvpn_easyrsa_email: "me@myhost.mydomain"
	openvpn_easyrsa_ou: "MyOrganizationalUnit"
	openvpn_easyrsa_name: "EasyRSA"
	openvpn_easyrsa_cn: "CommonName"
	
	
	# Default settings (See OpenVPN documentation)
	openvpn_host: "{{ inventory_hostname }}"           # The server address
	openvpn_port: 1194
	openvpn_proto: udp
	openvpn_dev: tun
	openvpn_server: 10.8.0.0 255.255.255.0              # Set empty for skip
	openvpn_bridge: no
	openvpn_configure_nat: no
	openvpn_max_clients: 100
	openvpn_log: /var/log/openvpn.log                   # Log's directory
	openvpn_keepalive: "10 120"
	openvpn_ifconfig_pool_persist: ipp.txt
	openvpn_comp_lzo: yes                               # Enable compression
	openvpn_cipher: BF-CBC                              # Encryption algorithm
	openvpn_status: openvpn-status.log
	openvpn_verb: 3
	openvpn_tls_auth : no                            # Enable perfect forward secracyxy
	openvpn_tls_key  : "ta.key"
	openvpn_user: openvpn
	openvpn_group: nobody
	openvpn_resolv_retry: infinite
	openvpn_client_to_client: no
	openvpn_verify_client_cert: no
	openvpn_client_options: []                          # Additional client options
	                                                    # openvpn_client_options:
	                                                    # - dev-node MyTap
	                                                    # - client-to-client
	# Use PAM authentication
	openvpn_use_pam: yes
	openvpn_use_pam_users: []                         # If empty use system users
	                                                  # otherwise use users from the option
	                                                  # openvpn_use_pam_users:
	                                                  # - { name: user, password: password }
	
	# LDAP authentication and configuration (optional)
	openvpn_use_ldap: no
	openvpn_ldap_tlsenable: 'no'
	openvpn_ldap_follow_referrals: 'no'
	
	# Use simple authentication (default is disabled)
	openvpn_simple_auth: no
	openvpn_simple_auth_password: ""
	
	# Whether to embed CA, cert, and key info inside client OVPN config file.
	openvpn_unified_client_profiles: no
	openvpn_server_options:
	  - push "redirect-gateway def1 bypass-dhcp"
	  - push "dhcp-option DNS 8.8.8.8"
	  - push "dhcp-option DNS 8.8.4.4"

Example Playbook
----------------

    - hosts: servers
      roles:
         - role: alexiscangelosi.openvpn
	       # Server Configuration
	       openvpn_local: "1.2.3.4"
	       openvpn_proto: "tcp"
	       # Client Configuration
	       openvpn_clients: 
	         - client01
	         - client02
	       tags: openvpn

License
-------

BSD


