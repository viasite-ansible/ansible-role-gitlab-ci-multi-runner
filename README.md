## Install gitlab-ci-multi-runner and manage runners

This role can be used to install [gitlab-ci-multi-runner](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner) and manage runners (register and unregister them as requested).

### Limitations

- runners' configuration cannot be changed after registration
- every runner should have a unique name even tough `gitlab-ci-multi-runner` allows to create multiple runners with the same name

### Usage

```
---
- hosts:
    - testhost
  become: yes
  vars:
    gitlab_multirunner:
      runners:
        - name: runner21
          state: present
          ci_server: https://gitlab.example/ci
          token: uJLVTcWMrsuYzhBn9Y1N
          executor: shell
          tags:
            - my1
            - my2
        - name: old-runner1
          state: absent
        - name: old-runner2
          state: absent
  roles:
    - gtrafimenkov.gitlab-ci-multi-runner
```

### Supported Platforms

At the moment only:

- Debian-based Linux distributions

### Supported Executors

`gitlab-ci-multi-runner` supports [multiple executors](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/tree/master/docs/executors), but these role supports only limited subset.

At the moment it is only:

- shell

### TODO

- add support for CentOS
- add integration tests
- support more executors
- make it possible to unregister existing runners

### License

MIT