# General

Chimera's linux distro configs for a new installations

> Use headings list to quickly jump to the section you need, Luke!

## Informational

### Common shortcuts

* :white_check_mark: - My default option for a tool where multiple options are available
* No checkmark - backup option for a tool (I consider switching to it probably or legacy tool). I shouldn't install it if I'm not sure I want to switch right now

### Basic ideas

1. Install via OS package managers (not *Flatpak* or *Snap*, god forbid) if possible
1. Copy only things that are necessary

### Ideas for improvement

1. Make symlinks to configs in the repo instead of copying files for easier sync between computers in the future
2. Turn it into a *bash* script

## Basics

### Prerequisites

Assuming *Debian*/*Ubuntu* and derivatives: #TODO

1. Install prerequisites

    ``` Bash
    sudo apt install build-essential wget curl gpg apt-transport-https git
    ```

1. Unfortunately, for now also install *Flatpak* and add FlatHub repo

    ``` Bash
    sudo apt install flatpak
    flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
    ```

1. Make `~/Projects`

    ``` Bash
    mkdir ~/Projects
    ```

1. Clone this repo there

    ``` Bash
    git clone git@github.com:RayChimera/configs.git && cd ~/Projects/configs
    ```

1. Following commands assume you are running them from `~/Projects/configs`

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

> Helix usage manual is [here](https://docs.helix-editor.com/usage.html)

1. [Install](https://docs.helix-editor.com/package-managers.html) *Helix*:

    * From PPA (`Ubuntu`):

    ``` Bash
    sudo add-apt-repository ppa:maveonair/helix-editor
    sudo apt update && sudo apt install helix
    ```

1. Copy Helix configs:

    ``` Bash
    cp -r configs/helix/ ~/.config/
    ```

### VSCode

> Don't forget to choose an appropriate profile in VSCode! Configs are synchronized via *GitHub* profile, *NOT* *Microsoft* one

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

> #TODO Check if this way of porting configs work at all

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

1. Copy configs

    ``` Bash
    cp configs/1Password/* /home/chimera/.config/1Password/settings/
    ```

## Installing important non-directly coding-related programs

### Firefox

> Configs are synchronized automatically

1. [Add](https://support.mozilla.org/en-US/kb/install-firefox-linux#w_install-firefox-deb-package-for-debian-based-distributions-recommended) the repo:

    ``` Bash
    sudo install -d -m 0755 /etc/apt/keyrings
    wget -q https://packages.mozilla.org/apt/repo-signing-key.gpg -O- | sudo tee /etc/apt/keyrings/packages.mozilla.org.asc > /dev/null
    gpg -n -q --import --import-options import-show /etc/apt/keyrings/packages.mozilla.org.asc | awk '/pub/{getline; gsub(/^ +| +$/,""); if($0 == "35BAA0B33E9EB396F59CA838C0BA5CE6DC6315A3") print "\nThe key fingerprint matches ("$0").\n"; else print "\nVerification failed: the fingerprint ("$0") does not match the expected one.\n"}'
    echo "deb [signed-by=/etc/apt/keyrings/packages.mozilla.org.asc] https://packages.mozilla.org/apt mozilla main" | sudo tee -a /etc/apt/sources.list.d/mozilla.list > /dev/null
    echo '
    Package: *
    Pin: origin packages.mozilla.org
    Pin-Priority: 1000
    ' | sudo tee /etc/apt/preferences.d/mozilla
    ```

1. Install Firefox

    ``` Bash
    sudo apt update && sudo apt install firefox
    ```

### Telegram

> Settings sync #TODO

1. Install via Flatpak

    ``` Bash
    flatpak install flathub org.telegram.desktop
    ```

### Spotify

> Not officially available in Russia, so I had to use [OMGUbuntu](https://www.omglinux.com/how-to-install-spotify-on-linux/). Configs sync is not required

1. Install the repo

    ``` Bash
    curl -sS https://download.spotify.com/debian/pubkey_C85668DF69375001.gpg | sudo gpg --dearmor --yes -o /etc/apt/trusted.gpg.d/spotify.gpg
    echo "deb <http://repository.spotify.com> stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list
    ```

2. Install Spotify

    ``` Bash
    sudo apt update && sudo apt install spotify-client
    ```

## Russia-specific

> #TODO HideMyName VPN
