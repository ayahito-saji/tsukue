# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SHELL
set -i

sudo apt-get update
sudo apt-get upgrade

sudo apt-get -y install build-essential libncursesw5-dev libgdbm-dev libc6-dev zlib1g-dev libsqlite3-dev tk-dev libssl-dev openssl libbz2-dev libreadline-dev

sudo apt-get -y install sqlite3 libsqlite3-dev
sudo apt-get -y install postgresql libpq-dev

curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
source ~/.bashrc
nvm install --lts
nvm alias default lts/*

git clone https://github.com/yyuu/pyenv.git ~/.pyenv
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init -)"' >> ~/.profile
source ~/.profile

pyenv install 3.6.0
pyenv global 3.6.0

sudo -u postgres psql -c "CREATE ROLE vagrant WITH CREATEDB LOGIN PASSWORD 'vagrant';"

SHELL

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-16.04"
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 5000, host: 5000
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.provision "shell", privileged: false, inline: $script
end
