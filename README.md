# Vagrant box

debian wheezy 7.6 from chef/debian-7.6. 

```ruby
$script = <<SCRIPT
echo "deb http://http.debian.net/debian wheezy main" > /etc/apt/sources.list
echo "deb http://http.debian.net/debian wheezy-backports main" >> /etc/apt/sources.list
echo "Installing utilities"
apt-get update -y -q > /dev/null 2>&1
apt-get install vim git-core -y -q > /dev/null 2>&1
apt-get install -t wheezy-backports linux-image-amd64 -y -qq > /dev/null 2>&1
echo "Installing nvm"
su vagrant -l -c "curl -sSL https://raw.githubusercontent.com/creationix/nvm/v0.16.1/install.sh | bash > /dev/null 2>&1"
su vagrant -l -c "curl -sSL https://gist.githubusercontent.com/diorahman/6726424f0c3224861891/raw/df30aee542cf78cedafc6aec78f6e0efd8f5c13b/delta.sh | bash > /dev/null 2>&1"
echo "Installing node"
su vagrant -l -c ". /home/vagrant/.nvm/nvm.sh; nvm install 0.10 > /dev/null 2>&1"
echo "Installing docker"
su vagrant -l -c "curl -sSL https://get.docker.io/ | sudo sh > /dev/null 2>&1"
SCRIPT
```