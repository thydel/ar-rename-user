Using a simple requirement file

```yaml
- src: https://github.com/thydel/ar-rename-user.git
  name: rename-user
  version: master
```

```
ansible-galaxy install -r requirement.yml 
```

Using [ansible-toolbox][], from a *playbook-dir* with a valid *inventory* and *roles_path*

```
ansible-role -GH node rename-user -e old=dupont -e new=dupond -C
```

This assume that the *user* `user` also has a associated primary *group* `user`.

[ansible-toolbox]: https://github.com/larsks/ansible-toolbox "github.com"
