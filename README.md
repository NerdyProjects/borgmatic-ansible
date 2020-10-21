Borgmatic Ansible
=========

This role provides a simple borgmatic setup that cares about installation and backups of files, in addition with backing up a MySQL or Postgres database and providing a prometheus metric.

Requirements
------------

The role will use the debian package manager, it is meant to be used on debian systems.

After running the role for the first time, you have to init the borgmatic repository yourself.

Run the following as root:

```
borgmatic --init --encryption keyfile
```

You might chose other options to your wish.

Other useful commands you might want to use:

```
#
# export key:
#  borg key export
#
# backup list:
#   borgmatic --list
#
# restore backup:
#   borgmatic --extract --archive dragonfruit-2019-06-07T16:47:36.547867 --restore-path ORIGINALPATH
```

Role Variables
--------------

`borg_encryption_passphrase`: The passphrase to be used for the backup


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    ---
    - name: holunder | backups
      hosts: holunder
      vars_files:
        - ../secrets.yml
      tasks:
        - name: backups
          include_role:
            name: backup
          vars:
            borg_repository: ssh://holunder-backup@server:12345/home/holunder-backup/storage/repo
            backup_folders:
              - /etc

            backup_mysql_databases: []

            backup_postgres_databases: 
              - greenlight

License
-------

BSD