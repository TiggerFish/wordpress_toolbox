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
* **wptb_update_firewall:** true | false Run the firewall play, see my earlier comments about it being pants.
* **wptb_loclan:** A list of local lan addresses or networks that will be given TCP port 22 access if the firewall play runs.
* **wptb_email:** Email address used for the letsencrypt transaction.
* **wptb_le_server:** The letsencrypt server to request the ssl certificates from.
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
