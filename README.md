# General

Chimera's linux distro configs for a new installations

> Use headings list to quickly jump to the section you need, Luke!

## Ideas

1. Make symlinks to configs in the repo instead of copying files for easier sync between computers in the future
2. Turn it into a *bash* script

## Common shortcuts

* :white_check_mark: - My default option for a tool where multiple options are available
* No checkmark - backup option for a tool (I consider switching to it probably or legacy tool). I shouldn't install it if I'm not sure I want to switch right now

## Basics

### Prerequisites

Assuming *Debian*/*Ubuntu* and derivatives: #TODO

1. Install prerequisites:

    ``` Bash
    sudo apt install build-essential wget curl gpg apt-transport-https git
    ```

1. Make `~/Projects`

    ``` Bash
    mkdir ~/Projects
    ```

### Shell

1. Install a shell (*zsh*/*fish*). Assuming *Debian*/*Ubuntu*:
```sudo apt install zsh fish```

2. Now choose between *zsh* and *fish* (checkmark shows default)

#### :white_check_mark: *zsh*

1. [Install](https://ohmyz.sh/#install) *oh-my-zsh* with *curl*:

    ``` Bash
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    ```

1. Copy *zsh* config from `~` to `~/.zshrc`:

    ``` Bash
    cp configs/zsh/.zshrc ~/.zshrc
    ```

1. [Install fonts](https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k)
1. Install *Powerlevel10k*

    ``` Bash
    git clone --depth=1 <https://github.com/romkatv/powerlevel10k.git> "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k"
    ```

1. Copy *Powerlevel10k* config:

``` Bash
cp configs/zsh/.p10k.zsh ~/.p10k.zsh
```

#### *fish*

1. Install fish:

    ``` Bash
    sudo apt install fish
    ```

    > #TODO

#### Continue with setting up shell

1. Get all shells paths:
```cat /etc/shells```

1. Set preferred shell:

* For *zsh*: `chsh -s /bin/zsh chimera`
* For *fish*: `chsh -s /usr/bin/fish chimera`

### Helix

1. [Install](https://docs.helix-editor.com/package-managers.html) *Helix*:

    * From PPA (`Ubuntu`):

    ``` Bash
    sudo add-apt-repository ppa:maveonair/helix-editor
    sudo apt update && sudo apt install helix
    ```

1. Copy Helix config: #TODO

### VSCode

> Don't forget to choose an appropriate profile in VSCode!

1. [Add](https://code.visualstudio.com/docs/setup/linux#_install-vs-code-on-linux) the repo:

    ``` Bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
    sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
    echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" |sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
    rm -f packages.microsoft.gpg
    ```

1. Install VSCode:

    ``` Bash
    sudo apt update && sudo apt install code
    ```

### 1Password

1. [Add](https://support.1password.com/install-linux/#debian-or-ubuntu) the repository

    ``` Bash
    curl -sS https://downloads.1password.com/linux/keys/1password.asc | sudo gpg --dearmor --output /usr/share/keyrings/1password-archive-keyring.gpg
    echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/1password-archive-keyring.gpg] https://downloads.1password.com/linux/debian/amd64 stable main' | sudo tee /etc/apt/sources.list.d/1password.list
    sudo mkdir -p /etc/debsig/policies/AC2D62742012EA22/
    curl -sS <https://downloads.1password.com/linux/debian/debsig/1password.pol> | sudo tee /etc/debsig/policies/AC2D62742012EA22/1password.pol
    sudo mkdir -p /usr/share/debsig/keyrings/AC2D62742012EA22
    curl -sS <https://downloads.1password.com/linux/keys/1password.asc> | sudo gpg --dearmor --output /usr/share/debsig/keyrings/AC2D62742012EA22/debsig.gpg
    ```

1. Install *1Password*

    ``` Bash
    sudo apt update && sudo apt install 1password
    ```

## Installing important non-directly coding-related programs

### Firefox

> #TODO

### Telegram

> #TODO

### Spotify

> #TODO
