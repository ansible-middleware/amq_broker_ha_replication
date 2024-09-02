# amq_broker_ha_replication

Provision and deploy via Ansible a Red Hat AMQ broker cluster with replication on three nodes.

### Use case for collection

The primary use case of the amq_broker_ha_replication collection is to install Red Hat AMQ Broker with high availability (HA) across multiple AWS virtual machines. This ensures that the messaging service is resilient, fault-tolerant, and capable of serving users even in the event of a failure.

### 0. prerequisites

* A region that will host the authentication service (ie. us-east-1 or us-west-2)
* An AWS account with permissions on `ec2` on said regions with default profile in $HOME/.aws/credentials that will be used to provision ec2 compute nodes
* TLS certificate for the desired brokers to have encrypted communication

### 1. create ansible.cfg

```
[defaults]
remote_user=ec2-user
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

Set the `token` to the value you get after authentication on automation hub.


### 2. install dependencies

The following command will download and install the dependencies.

    # pip install -r requirements.txt
    # ansible-galaxy collection install -r requirements.yml


### 3. create key pair

This key pair will be used by ansible to connect to the EC2 instances.

* Paste the path to the private key in ansible.cfg option `private_key_file`
* Copy the public key file to `files/id_rsa_aws.pub`


### 4. edit the configuration


### run the infra provisioning

Inside playbooks/roles path we have infra-up.yml and infra-down.yml run both according to you need.

### run the deployment of amq_broker

Inside playbooks/roles path we have deploy.yml playbook to deploy data_grid and rhbk.

## License

[Apache License Version 2.0](https://github.com/ansible-middleware/rhbk-datagrid-aws/blob/main/LICENSE)
