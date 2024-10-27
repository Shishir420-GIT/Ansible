# Handlers in Ansible


## Example 1: Without Handlers
This playbook performs the following:

Copies the RPM package from /tmp to the current directory.
Installs the RPM package on the controller node.
Starts the service after installation.
Stops the service after starting it.

### Explanation of Each Task:
Copy Task:
- The copy module copies the RPM package from /tmp to the current directory (./).
remote_src: yes
- specifies that the source file is already on the controller node, so it doesn’t fetch it from Ansible’s local machine.
Install Task:
- The yum module installs the RPM package from the copied location in the current directory.
- ```{{ rpm_package_path | basename }}``` extracts the file name from the full path, making it flexible for any RPM file.
Start and Stop Service:
- The service module manages the service's state, starting and stopping it as required.

### Usage Note:
Ensure the rpm_package_path and service_name variables match the actual file name and service name you intend to manage.

## Example 2: With Handlers
To incorporate handlers for starting and stopping the service, you can set up a notify directive in the tasks. Handlers are triggered only if a task changes (for example, if the RPM package is newly installed). This approach is more efficient and fits well within Ansible's event-driven model.

### Explanation:
Notify Directive: The notify directive is added to the Install the RPM package task. If this task results in a change (i.e., the RPM package is newly installed), it will trigger the Start Service handler.

### Handler for Starting and Stopping:
Start Service:
- Starts the specified service and includes a notify directive to trigger the Stop Service handler afterward.
Stop Service:
- Stops the service after it has been started.
Notes:
- Handler Chaining:
- - By using notify within handlers, Ansible ensures that the Stop Service handler only runs after the Start Service handler completes
- Idempotency:
- - Handlers will not run unless there is a change, which keeps the playbook idempotent.