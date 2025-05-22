# Informational

> Chimera's linux distro configs for new installations

## Basic ideas

1. Install via OS package managers (not *Flatpak* or *Snap*, god forbid) if possible
1. Copy only things that are necessary

## Ideas for improvement

* No at the moment

## Prerequisites for Ansible Way (tm)

1. Make sure Python is (pre-)installed ([Full info on how if you aren't sure](https://docs.python.org/3/using/unix.html), you don't need IDLE or anything else extra, just a basic *Python 3* package)

    ``` Bash
    sudo apt install python
    ```

1. Install Ansible (*not* `ansible-core`)

    ``` Bash
    sudo apt install ansible
    ```

1. You are ready to start now!

    > Of course, you can setup your inventory etc but it's not required if you are configuring `localhost`. All of the playbooks are in the `playbooks` folder, but you'll only need `playbooks/setup.yml`

    ``` Bash
    ansible-playbook playbooks/setup.yml --ask-become-pass
    ```

## Manual, Non-Ansible Way (tm)

You should just follow a manual on the [wiki](https://github.com/RayChimera/configs/wiki). Good luck!
