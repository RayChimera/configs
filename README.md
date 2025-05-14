# General

Chimera's linux distro configs for a new installations

> Idea: make symlinks to configs in the repo instead of copying files for easier sync between computers in the future

## Basics

### Prerequisites

Assuming *Debian*/*Ubuntu*: #TODO

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

    * If *zsh* is desired:
        1. [Install](https://ohmyz.sh/#install) *oh-my-zsh* with *curl*: 

            ``` Bash
            sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
            ```

        1. Copy *zsh* config from `~` to `~/.zshrc`:

            ``` Bash
            cp zsh/.zshrc ~/.zshrc
            ```

        1. [Install fonts](https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k)
        1. Install *Powerlevel10k*

            ``` Bash
            git clone --depth=1 <https://github.com/romkatv/powerlevel10k.git> "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k"
            ```

        1. Copy *Powerlevel10k* config:

        ``` Bash
        cp zsh/.p10k.zsh ~/.p10k.zsh
        ```

    * If *fish* is desired:
        > #TODO

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
    sudo apt update
    sudo apt install helix
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
    sudo apt update
    sudo apt install code
    ```

### 1Password

> #TODO

## Installing non-directly coding-related programs

### Firefox

> #TODO

### Telegram

> #TODO

### Spotify

> #TODO
