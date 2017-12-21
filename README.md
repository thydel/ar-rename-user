# What

Uses [usermod][] and [groupmod][] to rename an *user*

- [usermod][] will change the login name and move home directory
- [groupmod][] will change the group name

The role

- Assumes that the *user* `user` also has a associated primary *group*
  `user`.
- Requires a working `become` for `root` (via passwordless `sudo` or
  configured `ansible_become_pass` using [passwordstore][])
- Asserts that old user and group exist and that new user and group
  don't exists
- Don't assumes the home directory is in `/home` (i.e. computes new
  path from old)

[passwordstore]: https://docs.ansible.com/ansible/devel/plugins/lookup/passwordstore.html "docs.ansible.com"

Notes that [usermod][] correctly remames *user* in *group_name* from
`/etc/group`

[usermod]: http://man7.org/linux/man-pages/man8/usermod.8.html "man7.org"
[groupmod]: http://man7.org/linux/man-pages/man8/groupmod.8.html "man7.org"

# How

Using a simple requirement file

```yaml
- src: https://github.com/thydel/ar-rename-user.git
  name: rename-user
  version: master
```

```
ansible-galaxy install -r requirement.yml 
```

## Direct use

Using [ansible-toolbox][], from a *playbook-dir* with a valid
*inventory* and *roles_path* defined via `ansible.cfg`

```
ansible-role -GH a_node rename-user -e old=dupont -e new=dupond -C
```

[ansible-toolbox]: https://github.com/larsks/ansible-toolbox "github.com"

## Via playbook

Or Using [play.yml][] to first select *nodes* where *user* exists and
apply role (Still from a *playbook-dir* with a valid *inventory* and
*roles_path*)

```
roles/rename-user/play.yml -l a_group -e old=dupont -e new=dupond -C
```

[play.yml]: https://github.com/thydel/ar-rename-user/blob/master/play.yml "github.com"
