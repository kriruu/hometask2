Vagrant.configure("2") do |config|
  config.vm.define "vm1" do |vm1|
    vm1.vm.hostname = "vm1"
    vm1.vm.box = "ubuntu/focal64"
    vm1.vm.network "private_network", ip: "192.168.33.10"
    vm1.vm.network "forwarded_port", guest: 80, host: 8888

    vm1.vm.provider "virtualbox" do |vb|
      vb.name = "vm1"
      vb.gui = false
      vb.memory = "1024"
    end

    vm1.vm.provision "shell", run: "always", inline: <<-SHELL
        echo "Hello from the Ubuntu VM"
    SHELL
  end

  config.vm.define "vm2" do |vm2|
    vm2.vm.hostname = "vm2"
    vm2.vm.box = "centos/7"
    vm2.vm.network "private_network", ip: "192.168.33.20"
    vm2.vm.network "forwarded_port", guest: 84, host: 8884
    
    vm2.vm.provider "virtualbox" do |vb|
      vb.name = "vm2"
      vb.gui = false
      vb.memory = "1024"                        
    end

    vm2.vm.provision "shell", run: "always", inline: <<-SHELL
        echo "Hello from the CentOS VM"
        yum install -y epel-release
        yum install -y nginx
        systemctl start nginx               
        systemctl enable nginx
    SHELL
  end
  
end
