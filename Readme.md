## Setup

1. Install bins
```bash
# Arch Linux Family
sudo pacman -S texlive-most
# For Ubuntu, you might need a ppa:
sudo add-apt-repository ppa:jonathonf/texlive
sudo apt update && sudo apt install texlive-full
# Fedora
sudo dnf install texlive-scheme-full
# macOS MacTex Install
brew cask install mactex-no-gui
```

2. Install Vscode extension if applicable 
```bash
ext install latex-workshop
```

3. Make sure to build before releasing.
