Role Name
=========

An Ansible role that will build and maintain a single site wordpress installation on CentOS 7 and Fedora 29.

Requirements
------------

A host/guest with a basic install of CentOS 7 or Fedora 29 and an internet domain name with a host record that resolves to an external interface that can route traffic on TCP ports 80 and 443 to the host/guest.

Role Variables
--------------

# Database name for the wordpress database
wptb_msql_db: unusual_name

# Database username for the wordpress database
wptb_msql_user: somebody_else

# Database tab;e prefix
wptb_db_table_prefix: 'azAZ_'

# Firewall config. If update_firewall is set to false no firewall changes made
# loclan should be set to the IP address or netowrk that ssh should be restriced to
wptb_update_firewall: false
wptb_loclan: ['10.0.0.0/8', '192.168.0.0/16', '172.16.0.0/12']

# Email used for registration with letsencrypt and recovery contact.
wptb_email: "youremailaddress@somedomain"

# ACME Directory Resource URI. Use staging for testing
wptb_le_server: "https://acme-staging-v02.api.letsencrypt.org/directory"
#le_server: "https://acme-v02.api.letsencrypt.org/directory"

# Webserver hostname
wptb_site_cn: "hostname.internet.domain"
wptb_subj_alt_names: # Don't change the first value but you can add as many more as you like.
  - { type: 'DNS', value: '{{ wptb_site_cn }}'} # Don't change this
  - { type: 'DNS', value: 'other_hostname.internet.domain'} # Include this only if you need it, add more as required.

# Run/Configure backup routines
wptb_back_up: false
wptb_back_up_days_to_keep: '14' # 'n Days'
wptb_back_up_weeks_to_keep: '4' # 'n Weeks'
wptb_back_up_months_to_keep: '12' # 'n Months'
wptb_back_up_weekly_day: 'Monday' # 'Monday|Tuesday|Wednesday|Thursday|Friday|Saturday|Sunday'
wptb_back_up_monthly_date: '01' # 'DD'
wptb_back_up_yearly_date: ['01', '01'] # ['DD', 'MM']

#Patch the existing installation of wordpress
wptb_patch_it: false

# Restore wordpress
wptb_restore: false
wptb_restore_type: daily|weekly|monthly|yearly
wptb_restore_date: YYYY-MM-DD

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
