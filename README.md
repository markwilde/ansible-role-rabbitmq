# Ansible Role: RabbitMQ

A very basic ansible role for installing RabbitMQ on Ubuntu (only tested on 12.04).

Supports Clustering and High Availablity

## Requirements

The following firewall ports need to be open:

  - RabbitMQ: 5672
  - Management console: 15672 (if enabled)
  - Clustering: 4369, 25672 (if enabled)

## Example Configuration

```yaml
rabbitmq:

  config:

    cluster: true
    ulimit: 1024
    policies:
      - name: ha-all
        pattern: '^(?!amq\.).*'
        definitions:
          'ha-mode': 'all'

  plugins:

    - rabbitmq_management

  users:

    - user: admin
      password: password
      vhost: /
      configure_priv: .*
      read_priv: .*
      write_priv: .*
      tags: administrator
      state: present

    - user: guest
      state: absent

  vhosts: []
```