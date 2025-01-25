Prometheus Role
=========

This Ansible role sets up and configures Prometheus for monitoring, using Docker for containerized deployments. The role allows for flexible configuration through variables and integrates seamlessly with other monitoring tools.

Requirements
------------

- [Docker](https://docs.docker.com/engine/install/) - Docker must be installed on the target server.
- [Ansible](https://docs.ansible.com/) - Ansible must be installed to execute the playbook.

Role Variables
--------------

| Variable                        | Purpose                                                                 |
|----------------------------------|-------------------------------------------------------------------------|
| `prometheus_container_name`      | Defines the name of the Prometheus container.                           |
| `prometheus_scrape_interval`     | Defines the scrape interval for Prometheus (default: `15s`).            |
| `prometheus_port`                | Defines the port for Prometheus web interface (default: `9090`).        |
| `prometheus_jobs`                | List of scrape jobs with `name` and `targets` (e.g., `node_exporter`, `app_metrics`). |
| `prometheus_docker_network`      | Enables/disables Docker network for Prometheus (default: `false`).      |
| `prometheus_docker_network_name` | Name of the Docker network if `prometheus_docker_network` is enabled.   |

Dependencies
------------

This role has no external dependencies.

Example Playbook
----------------

Prometheus jobs declaration :

```
prometheus_jobs:
  - name: node_exporter
    targets:
      -  <ip>:9100
  - name: graphite_exporter
    targets:
      -  <ip>:9108
```

How to call the `role`: 

```
- name: Setup prometheus
  hosts: my_host 
  become: yes
  roles:
    - role: prometheus
      tags: prometheus
```

License
-------

BSD
