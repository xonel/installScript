### installScript
- Please use a new SD card if installing on an arm/sbc device.
- This script will install openmediavault, omv-extras, and flashmemory. If you already have openmediavault installed don't worry, your openmediavault will be preserved, only the not installed will be added to the system.
- Installing OMV with a desktop environment is NOT supported.  Please read the forum for the many reasons why.
- This script may alter previous network setups.  This has a greater chance of breaking wifi setup.  Please read the install manual for more help - https://wiki.omv-extras.org/

### Notes
- This script will always install
  - OMV 5.x on Debian 10 (Buster)
  - OMV 6.x on Debian 11 (Bullseye)

### Installation 
To install OMV, OMV-Extras and Flashmemory copy and paste this line in the Terminal and press Enter. The installation will take some time, so enjoy the text flying on the screen. 

***The installation process demands sudo utilization.***

To download and execute the script you can use either *wget* or *curl*, feel free to use what you prefer!

*wget script*
####  
```bash
sudo wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash
```

*curl script*
```bash
sudo curl -sSL https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash
```
### To skip network setup
If you don't wanna use the network setup steps of the script, please use copy and paste the followings lines to the terminal. 
```bash
wget https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install
chmod +x install
sudo ./install -n
```

### A detailed guide is available for this script as well
openmediavault is primarily designed to be used in home environments or small home offices, but is not limited to those scenarios. It is a simple and easy to use out-of-the-box solution that everyone can install and administer without needing expert level knowledge of Networking and Storage Systems.

The openmediavault documentation can be accessed in https://openmediavault.readthedocs.io/en/5.x/new_user_guide/newuserguide.html

And for the OMV-Extras visit https://wiki.omv-extras.org/
 
### Get help for this script in the forum
If you got stuck in any part of this script the openmediavault forum will be the place to find a solution https://forum.openmediavault.org/

----
https://didrod.blogspot.com/2020/02/installer-openmediavault-sur-un-serveur_69.html

```bash
cfdisk
fdisk -l

Device          Start        End    Sectors  Size Type
/dev/sda1        2048       4095       2048    1M BIOS boot
/dev/sda2        4096   40964095   40960000 19.5G Linux filesystem
/dev/sda3    40964096   42012671    1048576  512M Linux filesystem
/dev/sda4  3907025072 3907029134       4063    2M Linux filesystem

/dev/sda5    42012672 3907025071 3865012400  1.8T Linux filesystem

mkfs.ext4 /dev/sda5 


```

----
https://docs.openmediavault.org/en/stable/installation/on_debian.html


Install the openmediavault keyring manually:
```bash
apt-get install --yes gnupg
wget -O "/etc/apt/trusted.gpg.d/openmediavault-archive-keyring.asc" https://packages.openmediavault.org/public/archive.key
apt-key add "/etc/apt/trusted.gpg.d/openmediavault-archive-keyring.asc"
```
Add the package repositories:

```bash
cat <<EOF >> /etc/apt/sources.list.d/openmediavault.list
deb https://packages.openmediavault.org/public shaitan main
# deb https://downloads.sourceforge.net/project/openmediavault/packages shaitan main
## Uncomment the following line to add software from the proposed repository.
# deb https://packages.openmediavault.org/public shaitan-proposed main
# deb https://downloads.sourceforge.net/project/openmediavault/packages shaitan-proposed main
## This software is not part of OpenMediaVault, but is offered by third-party
## developers as a service to OpenMediaVault users.
# deb https://packages.openmediavault.org/public shaitan partner
# deb https://downloads.sourceforge.net/project/openmediavault/packages shaitan partner
EOF
```
Install the openmediavault package:

```bash
export LANG=C.UTF-8
export DEBIAN_FRONTEND=noninteractive
export APT_LISTCHANGES_FRONTEND=none
apt-get update
apt-get --yes --auto-remove --show-upgraded \
    --allow-downgrades --allow-change-held-packages \
    --no-install-recommends \
    --option DPkg::Options::="--force-confdef" \
    --option DPkg::Options::="--force-confold" \
    install openmediavault-keyring openmediavault

omv-confdbadm populate
```
