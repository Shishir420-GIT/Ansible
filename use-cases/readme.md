## Running the Playbook
To run either playbook, save it to a YAML file (e.g., get_cpu_utilization.yml) and execute it with the following command:
```
ansible-playbook -i inventory_file cpu_memory_utilization.yml
```
Make sure to replace inventory_file with your actual Ansible inventory file path. This will gather and display CPU and memory utilization for the hosts specified in your inventory.