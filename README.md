# amq_broker_ha_replication

Provision and deploy via Ansible a Red Hat AMQ broker cluster with replication on three nodes.

### Use case for collection

The primary use case of the amq_broker_ha_replication collection is to install Red Hat AMQ Broker with high availability (HA) across multiple virtual machines. This ensures that the messaging service is resilient, fault-tolerant, and capable of serving users even in the event of a failure.

### 0. prerequisites

* three virtual machines or containers with proper name resolution and network access.
* keypair ssh access to the virtual machines, with privilege escalation
* ansible-core >= 2.15

### 1. create ansible.cfg

```
[defaults]
remote_user=<ssh_user_account>
private_key_file=<path_to_private_key>
host_key_checking=False
gathering=smart
pipelining=True

[galaxy]
server_list=galaxy,automation_hub

[galaxy_server.galaxy]
url=https://galaxy.ansible.com/

[galaxy_server.automation_hub]
url=https://cloud.redhat.com/api/automation-hub/
auth_url=https://sso.redhat.com/auth/realms/redhat-external/protocol/openid-connect/token
token=<automation_hub_token>
```

1. Set the `token` to the value you get after authentication on automation hub.
2. Set <ssh_user_account> to the posix account that can ssh into the target virtual machines
3. Set <path_to_private_key> to the absolute path to the private key used for ssh


### 2. install dependencies

The following command will download and install the dependencies.

    # pip install -r requirements.txt
    # ansible-galaxy collection install -r requirements.yml


### 3. inventory

This key pair will be used by ansible to connect to the EC2 instances.

* Paste the path to the private key in ansible.cfg option `private_key_file`
* Copy the public key file to `files/id_rsa_aws.pub`


### 4. edit the configuration

#### install options

#### service options

#### run the deployment of amq_broker

Execute the install.yml playbook to deploy the amq_broker setup.


## License

[Apache License Version 2.0](https://github.com/ansible-middleware/rhbk-datagrid-aws/blob/main/LICENSE)
