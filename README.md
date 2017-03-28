# Ansible: Taskwarrior

Forked from: https://github.com/oleg-fiksel/ansible-taskd

This playbook's aim is to deploy and base configure a taskd server.
Currently it's working only with Ubuntu Server 16.04 (LTS).

This playbook doesn't handle the task (client) installation. Refer to http://taskwarrior.org/download/#setup for help.

**NOTE: THIS IS WIP, DO NOT USE YET.**

## Usage

### Install and configure taskd

Adjust variables, if needed, in `defaults/main.yml`

```
ansible-playbook -i taskd-server.domain, main.yml
```

### Add user (client)

```
ansible-playbook -i taskd-server.domain, add_user.yml -e 'taskd_org=Public taskd_client=testuser'
```

This will generate the certificates and download them into the fetch/ directory. Note - the auth file is not yet downloaded, WIP.


## TODO

- Install task client properly
  - package module
  - deploy auth file into ~/.task
- check config template, see if it matches prod.
- check config, see if it matches my smirnovlabs.


## Notes

- If you change cert vars, you will have to redo certificates and re-add users. Sorry, this is the way PKI works.

## Testing

- `vagrant up`
- `vagrant destroy`

# Links

* [http://taskwarrior.org/](Taskwarrior)
