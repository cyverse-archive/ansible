de-init-tool-permissions
=======================

Registers existing tools in the DE database in the permissions service.
All existing tools are considered public by the underlying utility,
which grants everyone in the de-users group `read` permissions on every tool.

Role Variables
--------------

| Name                   | Description                     | Required | Default                           |
| docker_tag             | Docker tag name                 | No       | {{ docker.tag | default(dev) }}   |
| tool_registration_repo | Tool registration docker repo   | No       | discoenv/tool-registration        |
| config_image_name      | Configuration docker image name | No       | de-configs-{{ environment_name }} |
| config_repo            | Configuration docker repo       | No       | {{ docker.registry.base }}/{{ config_image_name }} |
| config_path            | Configuration path              | No       | /etc/iplant/de/permissions.yaml   |
| de_database_name       | Name of the DE database         | No       | {{ db_name }}                     |

Example Playbook
----------------

    ---
    - name: initialize tool permissions
      hosts: permissions:&systems
      become: true
      gather_facts: false
      tags:
        - services
        - permissions
      roles:
        - role: de-init-tool-permissions

License
-------

BSD
