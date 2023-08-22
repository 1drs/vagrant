# vi: ft=ruby:ts=2:ai:sw=2
$script = <<-SCRIPT
echo "I am on provisioning, please wait....."
sudo cat /home/vagrant/sources.list > /etc/apt/sources.list
sudo apt update
sudo apt remove multipath-tools -y
sudo apt install nginx -y
sudo apt install mtr -y
SCRIPT
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.box_check_update = false
  config.vm.hostname = 'vm.jcolab.lan'
  config.vm.network "private_network", ip: "192.168.60.100", name: "vboxnet4"
  config.vm.provider "virtualbox" do |vb|
    vb.name = "sharing_session_VM"
    vb.gui = false
    vb.memory = "4096"
    vb.cpus = "2"
  end
  config.vm.provision "file", source: "<change_sources.list_path>", destination: "~/sources.list"
  config.vm.provision "shell", inline: $script
  config.vm.synced_folder "<change_sharing_folder_path>", "/data/"
end
