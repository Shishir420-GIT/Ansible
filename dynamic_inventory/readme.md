# Using or Creating a dynamic inventory

The add_host module in Ansible is used to dynamically add a host to the inventory during a playbook run. This is useful when you need to interact with hosts that aren’t initially in your inventory file or when you want to group hosts dynamically based on certain conditions during a playbook run.

Basic Syntax of add_host
```
- name: Add a host to inventory
  add_host:
    name: "{{ inventory_hostname }}"  # The name or IP of the host to add
    groups: "dynamic_group"           # The group to add this host to
    ansible_user: "new_user"          # Optional: define variables for the new host
```

## Example 1:  Playbook Using add_host
This playbook demonstrates:
- Adding a host dynamically.
- Running tasks on that newly added host in a separate play.

## Explanation of How add_host Works
- Add a Host to Inventory:
- - The add_host module is executed on the localhost machine (or wherever the play is running).
- - This adds the specified host (e.g., 192.168.1.100) to the group dynamic_group in the in-memory inventory.

- Define Variables for the New Host:
- - You can specify variables such as ansible_user, ansible_port, etc., directly within add_host.
- - These variables are applied only to the newly added host.

- Run Tasks on the New Host:
- - In the second play, the hosts directive is set to dynamic_group, so Ansible now treats 192.168.1.100 as part of the inventory.
- - This play will target and run tasks on the newly added host.

- When to Use add_host
- - Dynamic Host Addition:
- - - If you dynamically obtain IP addresses or hostnames during the playbook execution. You can use add_host to add these hosts to your inventory and interact with them immediately.

- - Dynamic Group Creation:
- - - If you want to create groups of hosts on the fly (e.g., only add web servers with specific configurations), add_host is ideal for that

- - Conditional Inclusion:
- - - Use add_host to include or exclude hosts from specific tasks or plays based on conditions.