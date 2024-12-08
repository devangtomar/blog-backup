---
title: "Setting Up a Mac for Development: A Comprehensive Guide 🧑🏻‍💻 ‍"
datePublished: Sun Nov 24 2024 09:46:34 GMT+0000 (Coordinated Universal Time)
cuid: cm3vfgkbq000h09l11b7khkif
slug: setting-up-a-mac-for-development-a-comprehensive-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1732442533893/79bf03b5-a2e4-4854-9a15-1f6d82c29608.jpeg

---

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732442373180/06f269d0-48db-4a8c-a892-5ae8275cd3a3.jpeg align="left")

Setting up a new Mac for development can be time-consuming, especially if you’re a developer who needs an efficient and tailored environment. Whether you’re setting up a work machine or a personal computer, having a checklist can save time and effort. Here’s a streamlined guide for getting your MacBook ready for development, optimized for macOS 15 (Sequoia).

### **Getting Started 🎬**

When you turn on your Mac, the setup assistant will guide you through basic configurations like selecting your language, time zone, and Apple ID. Once done, update macOS to ensure you have the latest security patches.

* [Install Homebrew for App Management ☕️](#d1d0)
    
* [Installing Essential Applications 📲](#4345)
    
* [Setting Up the Shell](#6b89)
    
* [Custom Brew Packages and Zsh Configuration](#85a2)
    
* [Configuring Git](#bacb)
    
* [Generate SSH Keys](#07bb)
    
* [Tuning macOS Settings](#0671)
    
* [Application-Specific Tips](#2cb2)
    

### **Install Homebrew for App Management ☕️**

[Homebrew](https://brew.sh/) is a must-have package manager for macOS, simplifying the installation of software.

Run the following command to install Homebrew:

```plaintext
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

After installation, ensure it’s updated:

```plaintext
brew update
```

### **Installing Essential Applications 📲**

Here’s a list of CLI tools and GUI applications you’ll likely need:

#### **Command-Line Tools**

Install these using Homebrew:

```plaintext
brew install git
```

#### **Graphical Applications**

Install these with the — cask flag:

```plaintext
brew install - cask \
visual-studio-code \
google-chrome \
firefox \
rectangle \
iterm2 \
docker \
discord \
slack \
spotify \
postgres \
obsidian \
todoist
```

> **Note** : Do not install Node.js via Homebrew. Use nvm for better version control (details below).

### **Setting Up the Shell**

macOS comes with zsh as the default shell. Enhance it with **Oh My Zsh** :

```plaintext
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

#### **Add Shortcuts**

Edit your ~/.zshrc file to include aliases for convenience. For example:

```plaintext
alias x86="env /usr/bin/arch -x86_64 /bin/zsh - login"
alias arm="env /usr/bin/arch -arm64 /bin/zsh - login"
```

### **Custom Brew Packages and Zsh Configuration**

To further enhance your development environment, you can reference and use custom configurations from my personal repository.

This repository contains my curated list of **brew packages** , **Zsh plugins** , and **shortcuts** to optimize productivity.

#### **Access the Repository**

[GitHub - devangtomar/zsh-settings: This repository is dedicated to storing and managing my custom Zsh settings and configurations ⚙️](https://github.com/devangtomar/zsh-settings)

From the repository, you can:

* Get a list of Homebrew packages I frequently use.
    
* Import my custom ~/.zshrc settings to streamline your shell experience.
    

Clone the repository to your local machine:

```plaintext
git clone https://github.com/devangtomar/zsh-settings.git
```

Navigate to the directory and explore the setup:

```plaintext
cd zsh-settings
```

Feel free to fork or adapt the configurations to match your workflow!

### **Configuring Git**

Set up your Git global configuration:

```plaintext
touch ~/.gitconfig
```

Add the following content to customize Git commands:

```plaintext
[user]
  name = Your Name
  email = your_email@example.com
[github]
  user = username
[alias]
  a = add
  cm = commit -m
  s = status
  p = push
  co = checkout
  fp = fetch --prune --all
  l = log --oneline --decorate --graph
[push]
 autoSetupRemote = true
```

With the above aliases, I can run git s instead of git status, for example. It will also automatically set up your remote, so you can do git push on a branch without specifying the upstream origin.

### **Generate SSH Keys**

Create an SSH key for authentication, Start ssh-agent and adding the key:

```plaintext
ssh-keygen -t ed25519 -C "your_email@example.com"
eval "$(ssh-agent -s)"
ssh-add - apple-use-keychain ~/.ssh/id_ed25519
```

For easier management, create an SSH config file (~/.ssh/config):

```plaintext
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519

Host myssh
  HostName example.com
  User user
  IdentityFile ~/.ssh/key.pem
```

Now just run the alias to connect.

```plaintext
ssh myssh
```

### **Tuning macOS Settings**

To improve productivity, adjust these macOS settings:

#### Sidebar

To get the Home folder in the finder, press CMD + SHIFT + H and drag the home folder to the sidebar.

#### General

* Make Google Chrome default browser
    

#### Dock

* Automatically hide and show Dock
    
* Show indicators for open applications
    

#### Keyboard

* Key Repeat -&gt; Fast
    
* Delay Until Repeat -&gt; Short
    
* Disable “Correct spelling automatically”
    
* Disable “Capitalize words automatically”
    
* Disable “Add period with double-space”
    
* Disable “Use smart quotes and dashes”
    

#### Security and Privacy

* Allow apps downloaded from App Store and identified developers
    
* Turn FileVault On (makes sure SSD is securely encrypted)
    

#### Sharing

* Change computer name
    
* Make sure all file sharing is disabled
    

#### Users & Groups

* Add “Rectangle” to Login items
    

#### Defaults

A few more commands to change some defaults.

```plaintext
# Show Library folder
chflags nohidden ~/Library
# Show hidden files
defaults write com.apple.finder AppleShowAllFiles YES
# Show path bar
defaults write com.apple.finder ShowPathbar -bool true
# Show status bar
defaults write com.apple.finder ShowStatusBar -bool true
# Prevent left and right swipe through history in Chrome
defaults write com.google.Chrome AppleEnableSwipeNavigateWithScrolls -bool false
```

### Application-Specific Tips

#### Chrome

* Install [uBlock Origin](https://chromewebstore.google.com/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm)
    
* Install [React DevTools](https://chromewebstore.google.com/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
    
* Install [Redux DevTools](https://chromewebstore.google.com/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en)
    
* Install [Duplicate Tab Shortcut](https://chromewebstore.google.com/detail/duplicate-tab-shortcut/klehggjefofgiajjfpoebdidnpjmljhb?hl=en)
    
* Settings -&gt; Set theme to “Dark”
    

#### Visual Studio Code

Press CMD + SHIFT + P and click "Install code command in PATH".

Now you can use code {file} to open any file in VSCode.

#### Extensions

* Install [Diverse Dye](https://marketplace.visualstudio.com/items?itemName=DevangTomar.vscode-diverse-dye)
    
* Install [GitLens](https://gitlens.amod.io/)
    
* Install [Highlight Matching Tag](https://marketplace.visualstudio.com/items?itemName=vincaslt.highlight-matching-tag)
    
* Install [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
    
* Install [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
    

#### Rectangle

* Full Screen: CMD + SHIFT + ' (prevents messing with other commands)
    
* Left Half: CMD + OPTION + LEFT
    
* Right Half: CMD + OPTION + RIGHT
    

#### iTerm2

For some reason, iTerm2 does not let you use ⌥ + ← and → to tab through words in the terminal by default. I found this article to fix it: [Use ⌥← and ⌥→ to jump forwards / backwards](https://coderwall.com/p/h6yfda/use-and-to-jump-forwards-backwards-words-in-iterm-2-on-os-x)

* Go to Profiles -&gt; Keys:
    
* Change ⌥← via "Send Escape Sequence" with b
    
* Change ⌥→ via "Send Escape Sequence" with f
    

### **Conclusion**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732442374382/125ea324-07a8-42d1-a4b6-64927ec2ede6.jpeg align="center")

This guide is designed to provide a quick, repeatable process for setting up a Mac for development. By automating installations and configuring settings upfront, you can focus on coding and productivity rather than setup hassles.

### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/@devangtomar)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on Dev.to: [devangtomar](https://dev.to/devangtomar)