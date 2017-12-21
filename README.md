Using a simple requirement file

```yaml
- src: https://github.com/thydel/ar-rename-user.git
  name: rename-user
  version: master
```

```
ansible-galaxy install -r requirement.yml 
```

Using [ansible-toolbox][], from a *playbook-dir* with a valid
*inventory* and *roles_path* defined via `ansible.cfg`

```
ansible-role -GH a_node rename-user -e old=dupont -e new=dupond -C
```

This assume that the *user* `user` also has a associated primary *group* `user`.

[ansible-toolbox]: https://github.com/larsks/ansible-toolbox "github.com"

Or Using [play.yml][] first select *nodes* where *user* exists
and apply role (Still from a *playbook-dir* with a valid *inventory*
and *roles_path*)

```
roles/rename-user/play.yml -l a_group -e old=dupont -e new=dupond -C
```

[play.yml]: https://github.com/thydel/ar-rename-user/blob/master/play.yml "github.com"
