Upgrade VirtualBox 6.x to VirtualBox 7.x on Ubuntu/Debian
Check Current VirtualBox Version
First confirm your current version of VirtualBox either via GUI or command line;

vboxmanage --version
Sample output;

6.1.40r154048
Or from VirtualBox manager GUI > help > About VirtualBox…

upgrade VirtualBox 6.x to VirtualBox 7.x on Ubuntu/Debian
So, how can you upgrade VirtualBox 6.x to VirtualBox 7.x on Ubuntu/Debian?

Uninstall Previous Versions of VirtualBox
Before you can proceed to upgrade VirtualBox 6.x to VirtualBox 7.x on Ubuntu/Debian, you need to uninstall the current version.

Stop running vms;

vboxmanage list runningvms | sed -r 's/.*\{(.*)\}/\1/' | \
xargs -L1 -I {} VBoxManage controlvm {} poweroff
Quit VirtualBox manager by pressing Ctrl+q on VirtualBox manager.

Or simply;

pkill VirtualBox
Next, remove VirtualBox Extension Package if installed;

sudo vboxmanage extpack uninstall "Oracle VM VirtualBox Extension Pack"
Then, uninstall virtualbox;

sudo apt remove --purge --auto-remove virtualbox virtualbox-6.1
Note that this wont remove the VirtualBox virtual machines on your host system.

Once the package removal is done, reboot the system;

sudo systemctl reboot -i
Upgrade VirtualBox 6.x to VirtualBox 7.x on Ubuntu/Debian
Once the system boots, proceed!

Next, install VirtualBox repository on your Ubuntu or Debian system if not already in place;


Play

Unmute
Remaining Time -0:49


Captions
Auto(360pLQ)
Share

Fullscreen
Upgrade VirtualBox 6.x to VirtualBox 7.x on Ubuntu/Debian
Upgrade VirtualBox 6.x to VirtualBox 7.x on Ubuntu/Debian
echo "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian $(lsb_release -sc) contrib" | \
sudo tee /etc/apt/sources.list.d/virtualbox.list
Install VirtualBox repository signing key;

sudo apt install gnupg2
wget -qO- https://www.virtualbox.org/download/oracle_vbox_2016.asc | \
sudo gpg --dearmor --yes -o /etc/apt/trusted.gpg.d/virtualbox.gpg
Run system package cache update;

sudo apt update
Install VirtualBox 7.x (VirtualBox 7.0 as of this writing is available) using the package manager.

sudo apt install virtualbox-7.0
Install VirtualBox Extension Pack for VirtualBox 7
Download VirtualBox 7.x extension pack and install;

wget -P /tmp https://download.virtualbox.org/virtualbox/7.0.2/Oracle_VM_VirtualBox_Extension_Pack-7.0.2.vbox-extpack
sudo vboxmanage extpack install --replace /tmp/Oracle_VM_VirtualBox_Extension_Pack-7.0.2.vbox-extpack
Launch VirtualBox 7.x on Ubuntu/Debian
You can now launch VirtualBox 7.x;

vboxmanage --version
