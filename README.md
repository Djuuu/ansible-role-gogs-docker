Ansible Role: Gogs-docker
=========================

Install Gogs Docker Compose project.

- https://gogs.io/
- https://github.com/gogs/gogs

Requirements
------------

Requires the following to be installed:
- docker
- docker compose

Role Variables
--------------

Common Docker projects variables:

```yaml
# Base directory for Docker projects
docker_projects_path: # /var/apps
```

Available role variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Docker project variables

gogs_project_name: gogs

# Docker project dynamic vars (uses `docker_project_name` prefix, adapt if overriden)

# Port targeted by Traefik router
gogs_traefik_loadbalancer_server_port: 3000

# Main service additional docker-compose options (ex: cpu_shares, deploy, ...)
gogs_compose_service_additional_options: |
  #ports:
  #  - "{{ gogs_http_port }}:3000"
  #  - "{{ gogs_ssh_port }}:22"
```

```yaml
# Gogs project variables

# gogs/gogs image version
gogs_version: latest

# Brand name of the application
gogs_brand_name: "Gogs"

# Public-facing domain for the application
gogs_domain: "gogs.local"

# Port bound to host for HTTP
gogs_http_port: 3000
# Port bound to host for SSH (also exposed in SSH clone URLs)
gogs_ssh_port: 8022

# Path to git repositories (mounted as a volume)
gogs_git_repositories: ./data/git/gogs-repositories

# Path to Gogs logs (mounted as a volume)
gogs_log_directory: ./data/gogs/log

# The secret to encrypt cookie values, 2FA code, etc.
# !!CHANGE THIS TO KEEP YOUR USER DATA SAFE!!
gogs_secret_key: CH4NGE ME !!!


# Database options

# The database backend, either "postgres", "mysql" "sqlite3" or "mssql".
gogs_database_type: sqlite3
gogs_database_host: 127.0.0.1
gogs_database_name: gogs
gogs_database_user: gogs
gogs_database_passwd: ''
# For "postgres" only
gogs_database_schema: public
# For "postgres" only, either "disable", "require" or "verify-full".
gogs_database_ssl_mode: disable
# For "sqlite3" only, make sure to use absolute path.
gogs_database_path: /data/gogs/data/gogs.db

# Email options

gogs_email_host:
gogs_email_from:
gogs_email_user:
gogs_email_passwd:

# Authentication options

# Whether to require email confirmation for adding new email addresses.
gogs_require_email_confirmation: true
# Whether to disallow anonymous users visiting the site.
gogs_require_signin_view: false
# Whether to disable self-registration. When disabled, accounts would have to be created by admins.
gogs_disable_registration: true
# Whether to enable captcha validation for registration
gogs_enable_registration_captcha: true

# Prometheus metrics authentication
gogs_basic_auth_username:
gogs_basic_auth_password:
```

Dependencies
------------

This role depends on :
- [djuuu.docker_project](https://github.com/Djuuu/ansible-role-docker-project)

Some variables allow integration with:
- [djuuu.traefik_docker](https://github.com/Djuuu/ansible-role-traefik-docker)

Example Playbook
----------------

```yaml
- hosts: all
  gather_facts: false

  roles:
    - djuuu.gogs_docker
```

License
-------

Beerware License
