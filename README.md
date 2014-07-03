Ansible playbooks example
=========================

Example usage of [creasty/ansible-roles](https://github.com/creasty/ansible-roles)


Directory structure
-------------------

```
├── group_vars
│   └── example_production.yml
├── hosts
├── ignitions
│   └── example_production.yml
└── roles
    ├── common
    └── example_production
        ├── files
        ├── tasks
        │   └── main.yml
        └── templates
```


How to use
----------

### 1. Get creasty/ansible-roles as submodule

```sh
$ git submodule add git@github.com:creasty/ansible-roles.git roles/common
```

I already did this for you, so insted of it, just clone the repository with recursive option.

```sh
$ git clone --recursive git@github.com:creasty/ansible-playbooks-example.git
```


### 2. A litte configuration in your playbook file

```yaml
# /ignitions/example_production.yml

  # ...

  vars:
    common_path:      ../../common
    assets_path:      ../roles/example_production
    loop_assets_path: ../example_production

  # ...
```

### 3. Edit parameters in a group vars file

```yaml
# /group_vars/example_production.yml

app:
  name: example
  path: /home/webapp/example

user:
  # ...
```

### 4. Include common roles in a main task file

```yaml
# /roles/example_production/tasks/main.yml

- include: '{{ common_path }}/common.yml'
- include: '{{ common_path }}/ntp.yml'
- include: '{{ common_path }}/user.yml'
- include: '{{ common_path }}/app.yml'
# ...
```

### 5. Run playbook

```sh
$ ansible-playbook -i hosts ignitions/example_production.yml
```

