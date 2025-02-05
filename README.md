# 🧑‍💻 dotfiles

My shell profile and CLI settings, geared towards backend dev/devops tooling.

The main purpose of this repo is to get up and running as fast as possible each time I install a new system. If you find anything useful in here, feel free to use it!

## ✨ Quick Start

> **NOTE:**
> - If you want to make your own adjustments, [fork](https://github.com/alexanderczigler/dotfiles/fork) this repository first and change the URL in step 1 below.
> - Backup your .zshrc and .gitconfig files before running the steps below, in case you want to revert back to any settings you currently have.

1. Clone this repo
  ```shell
  git clone https://github.com/alexanderczigler/dotfiles.git ~/.dotfiles
  ```
2. Bootstrap .zshrc
  ```shell
  echo ". ~/.dotfiles/.zshrc" > ~/.zshrc
  ```
3. Load .zshrc
  ```shell
  source ~/.zshrc
  ```
4. Configure GIT
  ```bash
  cat <<EOF > ~/.gitconfig
  [include]
    path = ~/.dotfiles/.gitconfig
  EOF
  ```

> You may need to force rebuild `zcompdump`:
> `rm -f ~/.zcompdump; compinit`
> 
> Additionally, if you receive "zsh compinit: insecure directories" warnings when attempting to load these completions, you may need to run these commands:
> - `chmod go-w '/opt/homebrew/share'`
> - `chmod -R go-w '/opt/homebrew/share/zsh'`

## 🍏 Mac OS

### 🍺 Homebrew

[Homebrew](https://brew.sh/) is a package manager for Mac OS that I recommend you use. With `brew` you can install several useful cli tools ranging from `awscli` to `direnv` and `kubectl`.

1. Install brew (instruction taken from https://brew.sh/)
  ```shell
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
  ```
2. Load brew into the current shell
  ```shell
  eval "$(/opt/homebrew/bin/brew shellenv)"
  ```

### 📦 Packages

#### Applications

```shell
# macOS
brew install --cask firefox obs spotify visual-studio-code
brew install microsoft-edge microsoft-outlook microsoft-teams

# linux
snap install bitwarden firefox discord spotify steam
snap install --classic code
sudo apt-get install jq yq telnet vim curl
```

#### CLI

```shell
# macOS
brew install colima direnv docker docker-buildx docker-compose fluxcd/tap/flux jq kubectl kubectx nvm opendevtools/supreme/supreme telnet watch yq
brew install bash-completion
brew install --cask google-cloud-sdk

# linux
snap install kubectl kubectx

# gcloud
gcloud --quiet components install beta gke-gcloud-auth-plugin
```

#### Fonts
```shell
brew tap homebrew/cask-fonts
brew install --cask font-fira-code
```

### ⚙️ Utilities

#### SensibleSideButtons

[SensibleSideButtons](https://sensible-side-buttons.archagon.net) will let you use the side buttons on a mouse just like in Linux or Windows. Once installed, add it to `Login items` in System Settings.

```shell
brew install --cask sensiblesidebuttons
```

> Once installed, add it to `Login items` in System Settings.

##### UnnaturalScrollWheels

[UnnaturalScrollWheels](https://github.com/ther0n/UnnaturalScrollWheels) lets you configure a _normal_ scroll direction on the wheel of a mouse, while keeping the _natural_ scroll direction on your trackpad. I love it!

```shell
brew install --cask unnaturalscrollwheels
```

> Once installed, add it to `Login items` in System Settings.

###### Configuration

![unnaturalscrollwheels](https://github.com/alexanderczigler/dotfiles/assets/3116043/b9b52edc-c7ea-4bcc-82ad-a66676784150)

#### hidutil

Remap `<` and `§` on my non-Apple keyboard.

##### Change this session only

```shell
sudo hidutil property --set '{"UserKeyMapping":[{"HIDKeyboardModifierMappingSrc":0x700000064,"HIDKeyboardModifierMappingDst":0x700000035},{"HIDKeyboardModifierMappingSrc":0x700000035,"HIDKeyboardModifierMappingDst":0x700000064}]}'
```

##### Persist change after reboot

Edit `~/Library/LaunchAgents/com.local.KeyRemapping.plist`

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.local.KeyRemapping</string>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/bin/hidutil</string>
        <string>property</string>
        <string>--set</string>
        <string>{"UserKeyMapping":[

            {
              "HIDKeyboardModifierMappingSrc": 0x700000064,
              "HIDKeyboardModifierMappingDst": 0x700000035
            },

            {
              "HIDKeyboardModifierMappingSrc": 0x700000035,
              "HIDKeyboardModifierMappingDst": 0x700000064
            }

        ]}</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
</dict>
</plist>
```
