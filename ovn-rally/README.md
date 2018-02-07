Instructions for installing OVN Scale Test (a plugin for Rally for OVN scale
testing) on Fedora 27.

Install Rally, modified for OVN testing, plus fixes for Fedora 27:

```
$ git clone https://github.com/jsitnicki/rally.git
$ cd rally
$ ./install_rally.sh
```

Install ovn-scale-test,a plugin for Rally, plus fixes for Fedora 27:

```
$ git clone https://github.com/jsitnicki/ovn-scale-test.git
$ cd rally
$ ./install_rally.sh
```

Create VMs using Vagrant+Ansible playbook:

```
$ git clone https://github.com/jsitnicki/vagrants
$ cd vagrants/ovn-rally
$ vagrant up
```

Update rally/deployments/ovn-multihost.json with your deployment details:
- IP addresses assigned management interface on each VM as reported by Vagrant,
- path to SSH key used by Vagrant

Activate Rally, create a deployments, and run a test scenario:

```
$ . ~/rally/bin/activate
$ rally-ovs deployment create --filename rally/deployments/ovn-multihost.json --name ovn-multihost
$ rally-ovs task start rally/scenarios/create-sandboxes.json
```

Generate the report by following the HINTS from 'rally-ovs task start' run.
