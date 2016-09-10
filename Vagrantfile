# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys DA1A4A13543B466853BAF164EB9B1D8886F44E2A
sudo touch /etc/apt/sources.list.d/openjdk.list
sudo echo "deb http://ppa.launchpad.net/openjdk-r/ppa/ubuntu trusty main " >>/etc/apt/sources.list.d/openjdk.list
sudo echo "deb-src http://ppa.launchpad.net/openjdk-r/ppa/ubuntu trusty main" >>/etc/apt/sources.list.d/openjdk.list

echo Installing dependencies...
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install -y unzip curl jq openjdk-8-jdk

export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
echo "$JAVA_HOME"

wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add ://packages.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
echo "deb https://packages.elastic.co/elasticsearch/2.x/debian stable main" | sudo tee -a /etc/apt/sources.list.d/elasticsearch-2.x.list
sudo apt-get update && sudo apt-get install -y --force-yes elasticsearch

echo "ES_JAVA_OPTS=-Djava.net.preferIPv4Stack=true" | sudo tee -a /etc/default/elasticsearch

SCRIPT


# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
#
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.provision "shell", inline: $script

  config.vm.define "es0" do |es0|
      es0.vm.hostname = "es0"
      es0.vm.network "private_network", ip: "172.20.20.50"
  end

  config.vm.define "es1" do |es1|
      es1.vm.hostname = "es1"
      es1.vm.network "private_network", ip: "172.20.20.51"
  end

  config.vm.define "es2" do |es2|
      es2.vm.hostname = "es2"
      es2.vm.network "private_network", ip: "172.20.20.52"
  end

end
