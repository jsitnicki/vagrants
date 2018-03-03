# How to run OVN Scale Test (a Rally plugin) on CentOS 7 or Fedora 27

Install a Rally fork modified for OVN testing:

```
$ git clone https://github.com/l8huang/rally.git
$ cd rally
$ ./install_rally.sh -d ~/rally-ovs-venv
```

Install ovn-scale-test, a plugin for Rally , plus fixes for CentOS/Fedora:

```
$ git clone https://github.com/jsitnicki/ovn-scale-test.git
$ cd ovn-scale-test
$ ./install.sh -d ~/rally-ovs-venv
```
Edit Vagrantfile to choose the distro for VMs.

```
DEFAULT_DISTRO = :centos
```

Create VMs using Vagrant + Ansible playbooks:

```
$ git clone https://github.com/jsitnicki/vagrants
$ cd vagrants/ovn-rally
$ vagrant up
```

Update `rally/deployments/ovn-multihost.json` with your deployment details:
- IP addresses assigned management interface on each VM as reported by Vagrant,
- path to SSH key used by Vagrant

Activate Rally, create a deployments, and run a test scenario:

```
$ . ~/rally-ovs-venv/bin/activate
$ rally-ovs deployment create --filename rally/deployments/ovn-multihost.json --name ovn-multihost
$ rally-ovs task start rally/scenarios/create-sandboxes.json
```

Generate the report by following the HINTS from `rally-ovs task start` run.
