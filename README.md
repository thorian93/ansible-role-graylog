# Ansible Role: Graylog

This role installs and configures the Graylog server on Debian and Ubuntu servers.

## Here be Dragons!

This role adds the Elasticsearch and MongoDB repositories to the managed system to install the necessary software. Make sure you are not breaking existing repository configuration with this!

## Requirements

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: foobar
      roles:
        - role: ansible-role-graylog
          become: yes

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    graylog_tunable_server_heap_size:         "1G"
    graylog_tunable_es_heap_size:             "1g"

Configure the amount of RAM Graylog itself and Elasticsearch may consume.

    graylog_tunable_es_jvm_custom_parameters: []

Add additional JVM options for elasticsearch.

    graylog_tunable_es_cluster_name:          "graylog"

Configure the Elasticsearch cluster name.

    graylog_tunable_mongodb_version:          "4.2"
    graylog_tunable_mongodb_featurecompatibilityversion: "4.0"

Configure MongoDB version to install and the FeatureCompatibilityVersion to set.

    graylog_tunable_version:                  "3.2"

Select which Graylog major version to install. *This is used to choose the appropriate repository, the minor version is as of now not selectable.*

    graylog_tunable_http_bind_port:           "9000"

Configure Graylog HTTP Port.

    graylog_tunable_http_bind_address:        "{{ ansible_default_ipv4.address }}"

Configure Graylog HTTP bind Adress.

    graylog_tunable_is_master:                "true"

Configure whether the Graylog node is the master. *For this role this should always be true.*

    graylog_tunable_password_secret:          []
    graylog_tunable_root_username:            "admin"
    graylog_tunable_root_password_sha2:       []
    graylog_tunable_root_email:               []
    graylog_tunable_root_timezone:            "UTC"

Configure basic settings like the admin account, secrets and timezone.

    graylog_tunable_http_proxy_uri:           ""
    graylog_tunable_non_proxy_hosts:          ""

Configure proxy settings if necessary.

## Dependencies

None.

## OS Compatibility

This role ensures that it is not used against unsupported or untested operating systems by checking, if the right distribution name and major version number are present in a dedicated variable named like `<role-name>_stable_os`. You can find the variable in the role's default variable file at `defaults/main.yml`:

    common_stable_os:
      - Debian 10
      - Ubuntu 18
      - CentOS 7
      - Fedora 30

If the combination of distribution and major version number do not match the target system, the role will fail. To allow the role to work add the distribution name and major version name to that variable and you are good to go. But please test the new combination first!

Kudos to [HarryHarcourt](https://github.com/HarryHarcourt) for this idea!

## Example Playbook

    ---
    - name: "Run role."
      hosts: all
      become: yes
      roles:
        - ansible-role-graylog

## Acknowledgements

This role is a simplified monolithical approach to installing a standalone Graylog server. It was inspired by the roles of the main projects involved:

- [Graylog](https://github.com/Graylog2/graylog-ansible-role)
- [Elasticsearch](https://github.com/elastic/ansible-elasticsearch)

## Contributing

Please feel free to open issues if you find any bugs, problems or if you see room for improvement. Also feel free to contact me anytime if you want to ask or discuss something.

## Disclaimer

This role is provided AS IS and I can and will not guarantee that the role works as intended, nor can I be accountable for any damage or misconfiguration done by this role. Study the role thoroughly before using it.

## License

MIT

## Author Information

This role was created in 2020 by [Thorian93](http://thorian93.de/).
