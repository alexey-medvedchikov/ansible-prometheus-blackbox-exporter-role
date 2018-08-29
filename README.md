# Ansible Role: prometheus-blackbox-exporter

An Ansible role that installs Prometheus BlackBox Exporter on Ubuntu|Debian|Redhat-based machines with systemd|Upstart|sysvinit.

## Requirements

All needed packages will be installed with this role.

## Role Variables

| Variable                                | Type   | Choices                           | Default                                                              | Comment                                                               |
|-----------------------------------------|--------|-----------------------------------|----------------------------------------------------------------------|-----------------------------------------------------------------------|
| prometheus_blackbox_exporter_version      | string | See [blackbox_exporter][1] releases | 0.12.0                                                              | Version of blackbox_exporter that will be installed.                    |
| prometheus_blackbox_exporter_release_name | string |                                   | blackbox_exporter-{{ prometheus_blackbox_exporter_version }}.linux-amd64 | Name of the binary that will be download from the [releases][1]) page |
| prometheus_blackbox_exporter_config_flags | dict   |                                   |                                                                      | Dict of key, value options to add to the start command line           |
| prometheus_blackbox_exporter_modules      | string |                                   |                                                                      | Contents of BlackBox configuration modules file                       |
| prometheus_blackbox_exporter_config_path  | string |                                   | {{ prometheus_exporters_common_conf_dir }}/blackbox-exporter/config.yaml | Path to store BlackBox modules configuration file                 |

## Dependencies

- UnderGreen.prometheus-exporters-common

## Example Playbook

```yaml
- hosts: blackbox-exporters
  roles:
    - role: alexey-medvedchikov.prometheus-blackbox-exporter
      prometheus_blackbox_exporter_version: 0.12.0
      prometheus_blackbox_exporter_config_flags:
        'web.listen-address': '9115'
      prometheus_blackbox_exporter_modules:
        http_2xx:
          prober: http
          timeout: 5s
          http:
```

## License

GPLv2

[1]: https://github.com/prometheus/blackbox_exporter/releases
