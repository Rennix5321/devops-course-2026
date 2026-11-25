# Учебный сервер

## 10. Ansible

Управляющий узел — Ubuntu в WSL, управляемый — Ubuntu Server в VirtualBox.
Плейбуки расположены в `ansible/`. Inventory `bootstrap.ini` использует
пользователя `student`, production inventory — `devops` и локальный SSH-ключ.

Роли: `base` устанавливает Docker, `ssh` настраивает учётную запись и UFW,
`nginx` настраивает reverse proxy, `app` запускает и проверяет приложение.

Образ `ghcr.io/rennix5321/devops-ci-app:fecd67640034c1a08059926023e74ade9e7ef56b` публикует контейнер
на loopback-порту 5000. Внешний запрос `/health` проходит через Nginx.

```sh
cd ansible
ansible-playbook -i inventory/bootstrap.ini site.yml --ask-pass --ask-become-pass
ansible-playbook site.yml
ansible-playbook verify.yml
```
