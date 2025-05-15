# General

## Informational

> Chimera's linux distro configs for new installations

### Navigation

Look at the navbar to the right and do each after another

### Common shortcuts

* :white_check_mark: - My default option for a tool where multiple options are available
* No checkmark - backup option for a tool (I consider switching to it probably or a legacy tool). I shouldn't install it if I'm not sure I want to switch right now

### Basic ideas

1. Install via OS package managers (not *Flatpak* or *Snap*, god forbid) if possible
1. Copy only things that are necessary

### Ideas for improvement

* No at the moment

### Prerequisites for Ansible Way (tm)

1. Make sure Python is installed (example for Debian derivatives, use `dnf` for Fedora/RHEL etc)

    ``` Bash
    sudo apt install python
    ```

1. Install Ansible (*not* `ansible-core`)

    ``` Bash
    sudo apt install ansible
    ```

1. You are ready to run playbooks now! (you can setup your inventory etc but it's not required if you are configuring `localhost`). All of the playbooks are in the `playbooks` folder. For example:

    ``` Bash
    ansible-playbook playbooks/setup.yml
    ```

### Manual, Non-Ansible Way (tm)

You should just follow a manual on the [wiki](https://github.com/RayChimera/configs/wiki). Good luck!
