# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
echo "deb http://kambing.ui.ac.id/debian wheezy main" > /etc/apt/sources.list
echo "deb http://kambing.ui.ac.id/debian wheezy-backports main" >> /etc/apt/sources.list
echo "Installing utilities"
apt-get update -y -q > /dev/null 2>&1
apt-get install vim build-essential libcurl3-gnutls liberror-perl -y -q > /dev/null 2>&1
apt-get install -t wheezy-backports linux-image-amd64 -y -qq > /dev/null 2>&1
echo "Installing git"
curl -sSL "https://cldup.com/ZK4KvDOpRJ.deb" >> /tmp/git-man.deb; dpkg -i /tmp/git-man.deb > /dev/null 2>&1
curl -sSL "https://cldup.com/cLegKVRFKg.deb" >> /tmp/git.deb; dpkg -i /tmp/git.deb >/dev/null 2>&1
rm -fr /tmp/*.deb
echo "Installing nvm"
su vagrant -l -c "curl -sSL https://raw.githubusercontent.com/creationix/nvm/v0.16.1/install.sh | bash > /dev/null 2>&1"
su vagrant -l -c "curl -sSL https://gist.githubusercontent.com/diorahman/6726424f0c3224861891/raw/df30aee542cf78cedafc6aec78f6e0efd8f5c13b/delta.sh | bash > /dev/null 2>&1"
echo "Installing node"
su vagrant -l -c ". /home/vagrant/.nvm/nvm.sh; nvm install 0.10 > /dev/null 2>&1"
su vagrant -l -c ". /home/vagrant/.nvm/nvm.sh; nvm alias default 0.10 > /dev/null 2>&1"
echo "Installing docker"
su vagrant -l -c "curl -sSL https://get.docker.io/ | sudo sh > /dev/null 2>&1"
SCRIPT

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "chef/debian-7.6"
  config.vm.box_url = "https://vagrantcloud.com/chef/boxes/debian-7.6/versions/1/providers/virtualbox.box"

  # specific ip
  config.vm.network "private_network", ip: "192.168.33.10"

  # nfs folder, mkdir ./dev first, or change it to another dir
  # smb for windows
  # config.vm.synced_folder "./dev", "/home/vagrant/share", type: "smb"
  config.vm.synced_folder "./dev" , "/home/vagrant/share", id: "vagrant", :nfs => true, :mount_options => ['nolock,vers=3,udp']

  # provisioner
  config.vm.provision "shell", inline: $script
end
