# Ansible MOTD Role

This is the Ansible MOTD role. It's designed for consumption by playbooks, not for consumption by itself.
It modifies the /etc/motd file to include a message that warns the user that SSH is probably not the best tool to
action their desired change, and lists alternative places that it's better to look.

## Usage

Include this in another ansible playbook. For sample, consider a generic server playbook:

```yaml
---
# $PLAYBOOK_ROOT/server.yaml
- name: "server"
  hosts: all
  become: true
  become_user: "root"
```

Add the reference for the role:

```yaml
# $PLAYBOOK_ROOT/server.yaml
# ...
become_user: "root"
roles
  - "motd"
```

This will allow the role to be discovered. Then, add this repo as a submodule:

```bash
$ cd path/to/playbook/root
$ mkdir roles/
$ git submodule add https://github.com/littlemanco/ansible-role-motd roles/motd
```

This should work! However, it will not list any places to look. To do so, add vars to the hosts that list the places:

```yaml
# $PLAYBOOK_ROOT/group_vars/$GROUP.yaml
---
motd_urls:
  - message: "Server setup is managed by ansible. See:"
    url: "https://github.com/littlemanco/ansible-playbook-server"
```

That's it!
