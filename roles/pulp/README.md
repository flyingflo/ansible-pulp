Pulp3
=====

Ansible role that installs Pulp 3 from PyPi or source and provides basic config.

The default administrative user for the Pulp application is: 'admin'

Role Variables:
---------------

* `pulp_cache_dir`: Location of Pulp cache. Defaults to "/var/lib/pulp/tmp".
* `pulp_config_dir`: Directory which will contain Pulp configuration files.
  Defaults to "/etc/pulp".
* `pulp_db_type`: Type of db to install packages for. Options are postgres
  or mysql. Default is postgres.
* `pulp_default_admin_password`: Initial password for the Pulp admin. **Required**.
* `pulp_install_dir`: Location of a virtual environment for Pulp and its Python
  dependencies. Defaults to "/usr/local/lib/pulp".
* `pulp_install_plugins`: A nested dictionary of plugin configuration options.
  Defaults to "{}", which will not install any plugins.
  * Dictionary Key: The pip installable plugin name. This is defined in each
  plugin's* `setup.py`. **Required**.
  * `app_label`: Used to make migrations. This is defined in the
  [PluginAppConfig](https://github.com/pulp/pulp_file/blob/76cc979e67fde128f78f3274697a4ea78f2269ec/pulp_file/app/__init__.py#L10)
  of each plugin. **Required**.
  * `source_dir`: Optional. Absolute path to the plugin source code. If present,
  plugin will be installed from source in editable mode.
* `pulp_install_api_service`: Whether to create systemd service files for
  pulp-api. Defaults to "true".
* `pulp_secret_key`: **Required**. Pulp's Django application `SECRET_KEY`.
* `pulp_source_dir`: Optional. Absolute path to Pulp source code. If present, Pulp
  will be installed from source in editable mode.
* `pulp_user`: User that owns and runs Pulp. Defaults to "pulp".
* `pulp_var_dir`: This will be the home directory of the created `pulp_user`.
  Defaults to "/var/lib/pulp".
* `pulp_use_system_wide_pkgs` Use python system-wide packages. Defaults to "false".
* `pulp_remote_user_environ_name` Optional. Set the `REMOTE_USER_ENVIRON_NAME` setting for Pulp.
* `pulp_content_host`: Host and port where Pulp content app is served. Defaults to `127.0.0.1:24816`
  This variable will be set as the value of `CONTENT_HOST` as the base path to build content URLs.
* `pulp_api_bind` Interface and Port where Pulp Content `gunicorn` service will listen. Defaults to
  '127.0.0.1:24817'. This variable is the value used to render the `pulp-api.service.j2` template
  passing to the `--bind` parameter of the `gunicorn` service.



Shared Variables:
-----------------

* `ansible_python_interpreter`: **Required**. Path to the Python interpreter.

This role is required by the `pulp-postgresql` role and uses variables that
are defined and documented in that role:

* `pulp_database_config`


Operating System Variables:
---------------------------

Each currently supported operating system has a matching file in the "vars"
directory.

License
-------

GPLv2

Author Information
------------------

Pulp Team
