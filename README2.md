# Spreedly Systems Engineer Work Sample - Consul



### The Task

Stand-up a cluster of Consul servers, as per the Spreedly work sample instructions.



### The Solution

Given the premise of needing to install, configure, and run Consul on pre-existing virtual machines, Ansible was selected as the primary tool for implementing a solution. 

In order to run this code, Ansible 2.4 or later is required on the system running this Ansible playbook, and every target machine must be reachable via ssh and have Python 2.x available.  In addition, the target servers should be able to freely communicate with each other across the local network (via private IP), and port 8500 should be exposed to the world in order to view the Consul web UI.

Before running this code, the Ansible configuration files `ansible.cfg` and `hosts` should be reviewed as explained below.  In addition, Consul installation defaults can be viewed or adjusted in the `vars` section of `main.yml`, although modifying these is not generally required for a successful execution.

The primary settings to be reviewed in `ansible.cfg` are as follows:

* `remote_user`: defaults to `root`, may need to be changed according to the target machines
* `private_key_file`: enter the full path to the private ssh key Ansible should use to connect to the target machines.  

The user and key file can also be specified on the command line, as shown in the examples below.

The `hosts` file defines a list of servers in the `consul` group, pre-configured to target the Digital Ocean VMs given in the work sample definition.  This group only needs to be modified if different targets are desired.



### Example Invocations

Below are some examples of how to run this playbook with Ansible.  The assumption is that all of the solution files are unpacked into your current working directory.

```
# default 
ansible-playbook main.yml -i hosts

# specify ssh key 
ansible-playbook main.yml -i hosts --key-file=/secret/key.pem

# specify ssh user 
ansible-playbook main.yml -i hosts --user=tarfu

# for more compact output, or to have less fun, the cows can be turned off
ANSIBLE_NOCOWS=1 ansible-playbook main.yml -i hosts

```



### Web UI

This playbook has already been executed on the Digital Ocean VMs provisioned for this exercise, and the following web UI links are available:

​	http://165.227.198.226:8500/ui

​	http://174.138.47.35:8500/ui

​	http://165.227.194.44:8500/ui

At the end of every execution, Ansible will output similar links to the web UIs for the newly provisioned instances.

For more information about the playbook, please review the code and comments in the YML files.



### Possible Future Improvements

* re-factor the Ansible code to use Ansible roles
* create separate roles for Consul server and Consul client
* add support for Consul services and health checks
* add support for configuring cluster auto-join with cloud metadata
* implement as immutable infrastructure instead of performing CM on pre-existing instances

















