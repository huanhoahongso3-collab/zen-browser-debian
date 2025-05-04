# Zen Browser Debian
This repository contains unofficial deb packages of the [zen browser](https://zen-browser.app/). As well as 
instructions on how to build the deb packages from the official tarballs. 

It is basically an attempt to reverse engineer the provided install script
for the zen browser, found at the link below for the purpose of creating deb packages.
[https://updates.zen-browser.app/install.sh](https://updates.zen-browser.app/install.sh)

## Steps to recreate
1. Clone this repository and enter the folder
```bash 
git clone https://github.com/huanhoahongso3-collab/zen-browser-debian.git & cd zen-browser-debian
```

2. Get the latest official tarball for the zen-browser from [here](https://github.com/zen-browser/desktop/releases). 
```bash
wget https://github.com/zen-browser/desktop/releases/latest/download/zen.linux-x86_64.tar.xz
```

3. Look through the variables at the top of the create-zen-deb.sh script, you
   should only really need to possibly the tarball name
```bash
PACKAGE_NAME="zen-browser"
VERSION="1.11.2b" # Changed in fork, no need to edit
ARCH="amd64"
TARBALL="zen.linux-x86_64.tar.xz"
BUILD_DIR="${PACKAGE_NAME}_${VERSION}"
INSTALL_DIR="$BUILD_DIR/opt/zen"
BIN_DIR="$BUILD_DIR/usr/local/bin"
DESKTOP_DIR="$BUILD_DIR/usr/local/share/applications"
```

4. Run the script
```bash
./create-zen-deb.sh
```
If everything goes to plan, you should now have .deb file in your folder. This
can then be installed with dpkg or uploaded to apt repo.

```
dpkg -i name-of-file.deb
```

You can also download an already built deb file from the releases section and
install it in the same way. 


## How to install using APT?
1. Add huanhoahongso3-collab's GPG Key:
```
wget -O- https://apt.fury.io/huanhoahongso3-collab/gpg.key | gpg --dearmor | sudo tee /usr/share/keyrings/fury.gpg > /dev/null
```
2. Add the following line to file: /etc/apt/sources.list.d/fury.list (create if not existed):
```
echo "deb https://apt.fury.io/huanhoahongso3-collab * *" | sudo tee /etc/apt/sources.list.d/fury.list > /dev/null
```
3. Install Zen Browser via APT
```
sudo apt update && sudo apt install zen-browser
```
Note: You may need to reboot for the Zen logo to appear normally
