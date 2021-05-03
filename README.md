# lihu-ansible

Set up your workstation like to look like mine.

## Setup

The DNF python bindings are unfortunately only available as an RPM at this moment; they are
not on pypi. So, in order to use them, we must make the system site packages available to
the virtualenv in which ansible is running. Poetry has an option to do this, but as of writing
this, the feature is only on master, which appears to have other bugs. Luckily, configuring
this manually is surprisingly easy. After running `poetry install`, simply edit the
`pyvenv.cfg` file in the created virtualenv:

```
include-system-site-packages = true
```

## Running the playbooks

The general command for executing the playbooks in this repo is

```
poetry run ansible-playbook playbooks/<playbook_name> -K
```

The `-K` flag will prompt you for the password for local privilege escalation, which is
necessary for many tasks. The playbook that includes every playbook in order is called
`everything.yml`.

If a task is hanging, there's a good chances you typed the password incorrectly and
Ansible is hanging at a sudo prompt.
