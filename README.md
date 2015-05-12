Ansible: Python App Deploy
==========================

Web application deployment role for ansible.

WIP: porting from several ad-hoc roles... expecting to
continue to do some major refactoring


Example Usage
--------------

```yaml
- name: App deploy
  serial: 1
  hosts: ...
  user: ...
  sudo: False
  roles: 
    - { role: deploy, app_name: 'APP_KEY' }
```


Example Settings
----------------

```yaml
apps:
    APP_KEY:
        build_steps: 
          - nodejs
          - django
        name: ???
        user: ubuntu
        server_name: "{{ENVIRONMENT}}.{{public_domain}}"
        deploy_rsa_key: "..."

        root: "{{apps_root}}/???"
        log_root: "{{apps_log_root}}/???"
        src_root: "{{apps_root}}/???/src"
        venv_root: "{{apps_root}}/???/venv"

        # src control stuff
        repo_url: ...
        repo_branch: master
        repo_remote: origin

        venv_base_libs:
          - gevent
          - git+https://github.com/circus-tent/chaussette.git#egg=chaussette-1.2-py2.7

        nginx_app_conf_tmpl: nginx-....conf.j2
        python_app_conf_tmpl: django-settings.py.j2
        python_app_conf_dest: "{{app_src_root}}/???/settings/{{ENVIRONMENT}}.py"

        # app/deploy path stuff
        managepy_path: "{{apps_root}}/???/src/manage.py"
        run_command: "{{apps_root}}/???/venv/bin/chaussette"
        run_args: "--fd $(circus.sockets.???) --backend gevent ???.wsgi.application"
        run_port: 8080
        chaussette_num_processes: 3
        chaussette_entry_point: "???.wsgi.application"
        wsgi_path: "{{apps_root}}/???/src/???/wsgi.py"
        venv_pip_path: "{{apps_root}}/???/venv/bin/pip"
        venv_python_path: "{{apps_root}}/???/venv/bin/python"

        # general environment vars
        environment:
          DJANGO_SETTINGS_MODULE: "???.settings.{{ENVIRONMENT}}"
          PYTHONPATH: "{{apps_root}}/???/src"
          NODE_ENV: production

        # app db
        dbname: ...
        dbuser: ...
        dbpassword: ...

        # ad-hoc app settings stuff

        email_host: ...
        email_user: ...
        email_password: ...
        email_port: 587

        cache_host: ...
        s3_bucket: "..."
        aws_key_id: ...
        aws_access_key: ...
        media_domain: ...

        linkedin_oauth_key: '...'
        linkedin_oauth_secret: '...'
        salesforce_oauth_key: '...'
        salesforce_oauth_secret: '...'

```
