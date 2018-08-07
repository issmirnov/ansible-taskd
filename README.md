# Ansible: Taskwarrior

Forked from: https://github.com/oleg-fiksel/ansible-taskd

This playbook will configure a [taskd server](https://taskwarrior.org/docs/taskserver/configure.html), and can add users as well. Tested on Ubuntu 16.04 as server, Ubuntu 16.04 + Mac OSX as the clients.


## Usage

1. Create your hosts file

```
[server]
task.yourserver.com

[clients]
laptop ansible_connection=local
desktop ansible_user=dev

```

2. Set up your variables in `vars/main.yml`
3. Set your sudo password with `ansible-vault edit vars/Debian.vault.yml` and `ansible-vault edit vars/Darwin.vault.yml`
4. Run the playbook: `ansible-playbook main.yml`

If at a later time you would like to just add a user, you can run: `ansible-playbook add_user.yml`. The server playbook is idempotent though, so you don't risk anything by running it more than once.


## Explanation

The add_user role will download the `auth` file, as well as the CA and client certs and sync them to all defined clients. The sample `taskrc` is very minimal, and contains to opinions on task config. It is meant to be used with a [modular config](https://github.com/issmirnov/dotfiles/blob/master/taskwarrior/taskrc). In order to avoid data loss, this playbook will not overwrite existing files.


## Notes

- If you change certificate variables, you will have to redo certificates and re-add users. Sorry, this is the way PKI works.
- If you already have a task server and are switching, run `task sync init` after running the playbook, then a `task sync`. This should clear up any issues such as `500 Client sync key not found.` or `No common ancestor`

## Testing

We use vagrant to test. The test.yml file uses vars from `vars/test_vars.yml`.  

- `vagrant up` - will create a new box
- `vagrant destroy` - will reset the box

# Links

- [http://taskwarrior.org/](Taskwarrior)
- [Ansible on Vagrant](https://www.vagrantup.com/docs/provisioning/ansible.html)
