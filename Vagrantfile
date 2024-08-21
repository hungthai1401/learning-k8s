Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"
     
  config.vm.provider "vmware_desktop" do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end
  
  config.vm.define "master" do |master|
    master.vm.network "private_network", ip: "192.168.50.10"
    master.vm.hostname = "master"
    master.vm.provider "vmware_desktop" do |vb|
      vb.name = "master"
    end
    master.vm.provision "shell", path: "./scripts/bootstrap.sh"
  end

  (1..2).each do |i|
    config.vm.define "node-#{i}" do |node|
      node.vm.network "private_network", ip: "192.168.50.#{10 + i}"
      node.vm.hostname = "node-#{i}"
      node.vm.provider "vmware_desktop" do |vb|
        vb.name = "node-#{i}"
      end
      node.vm.provision "shell", path: "./scripts/bootstrap.sh"
    end
  end
end