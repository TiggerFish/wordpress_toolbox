wordpress_toolbox
=========

An Ansible role that will build and maintain a single site wordpress installation on CentOS 7 and Fedora 29.

Features
------------
1. Installs all required components
2. Updates firewall (If you really want it to)
3. Gets and maintains ssl certs from letsencrypt
4. Backup & Restore
5. WordPress updates

Requirements
------------

A host/guest with a basic install of CentOS 7 or Fedora 29 and an internet domain name with a host record that resolves to an external interface that can route traffic on TCP ports 80 and 443 to the host/guest.

Role Variables
--------------

* **wptb_msql_db:** The name for the wordpress database.
* **wptb_msql_user:** The name of the user for the wordpress database.
* **wptb_db_table_prefix:** The prefix for the wordpress database table names.
* **wptb_update_firewall:** true | false Run the firewall play, yes or no.
* **wptb_loclan:** A list of local lan addresses or networks that will be given TCP port 22 access if the firewall play runs.
* **wptb_email:** Email address used for the letsencrypt transaction.
* **wptb_le_server:** The letsencrypt server to request the ssl certificates from.
* **wptb_le_force:** yes|no to force an early letsencrypt certificate request.
* **wptb_site_cn:** The common name (public hostname) of your webserver used for the letsencrypt transaction and the apache configuration.
* **wptb_subj_alt_names:** Subject alternate names for your website used for the letsencrypt transaction and the apache configuration.
* **wptb_back_up:** true | false Run the backup routine yes or no.
* **wptb_back_up_days_to_keep:** How long to keep daily backups in days.
* **wptb_back_up_weeks_to_keep:** How long to keep weekly backups in weeks.
* **wptb_back_up_months_to_keep:** How long to keep monthly backups in months.
* **wptb_back_up_weekly_day:** What day of the week weekly backups are taken.
* **wptb_back_up_monthly_date:** What day in the month monthly backups are taken.
* **wptb_back_up_yearly_date:** What date in the year yearly backups are taken.
* **wptb_msql_root_pw:** root password for the maria db. Note this var is in vars/main.yml and this file should be encrypted by vault or some other similar technology.
* **wptb_wp_msql_pw:** password for the wordpress database. Note this var is in vars/main.yml and this file should be encrypted by vault or some other similar technology.


Dependencies
------------

None, this role is self contained.

Example Playbook
----------------

```---
- name: Install wordpress_toolbox role
  hosts: all
  become: yes

  roles: 
    - role: wordpress_toolbox
      wptb_msql_root_pw: *hJdt*Yt*p+v&D/j-L+Eqpo
      wptb_wp_msql_pw: h%iek%NeRLbMm^\z4k>is
      wptb_wp_msql_db: wpdbuser
      wptb_db_table_prefix: az_AZ
      wptb_wp_msql_user: Ididntdoit
      wptb_update_firewall: false
      wptb_loclan: ['10.0.0.0/8', '192.168.0.0/16', '172.16.0.0/12']
      wptb_email: "youremailaddress@youremaildomain.com"
#      wptb_le_server: "https://acme-staging-v02.api.letsencrypt.org/directory"
      wptb_le_server: "https://acme-v02.api.letsencrypt.org/directory"
      wptb_le_force: no
      wptb_site_cn: "hostname.internetdomain.com"
      wptb_subj_alt_names:
        - { type: 'DNS', value: '{{ wptb_site_cn }}'}
        - { type: 'DNS', value: 'alias.internetdomain.com'}
      wptb_back_up: true
      wptb_back_up_days_to_keep: '14' # 'n Days'
      wptb_back_up_weeks_to_keep: '4' # 'n Weeks'
      wptb_back_up_months_to_keep: '12' # 'n Months'
      wptb_back_up_weekly_day: 'Friday' # 'Monday|Tuesday|Wednesday|Thursday|Friday|Saturday|Sunday'
      wptb_back_up_monthly_date: '01'
      wptb_back_up_yearly_date: ['01', '01'] # ['DD', 'MM']
      wptb_patch_it: false
      wptb_restore: false
      wptb_restore_type: daily
      wptb_restore_date: 2019-03-26
```      

Revisions
-------
27/04/19
Updated the redirect to SSL method so that letsencrypt challenge requests aren't redirected to the https webroot.
Added wptb_le_force variable to enable out of schedule (early) certificaate requests.
Added function to clean up the .well-known/acme-challenge directory.


License
-------

GPL-3.0

Author Information
------------------

TiggerFish https://www.bluegreenpla.net/index.php/wordpress_toolbox/
