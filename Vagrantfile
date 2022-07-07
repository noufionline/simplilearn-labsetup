Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |v|
      v.memory = 8192
      v.cpus = 4
  end

  config.vm.define "worker1" do | ubuntu |
      ubuntu.vm.box = "ubuntu/jammy64"
      ubuntu.vm.network "private_network", ip: "192.168.50.3"
      ubuntu.vm.hostname = "worker1"
      ubuntu.vm.provision "ansible", playbook: "deploy.yaml"
  end

  config.vm.define "worker2" do | ubuntu |
      ubuntu.vm.box = "ubuntu/jammy64"
      ubuntu.vm.network "private_network", ip: "192.168.50.4"
      ubuntu.vm.provision "ansible", playbook: "deploy.yaml"
      ubuntu.vm.hostname = "worker2"
  end
  
  config.vm.define "master" do | ubuntu |
      ubuntu.vm.box = "ubuntu/jammy64"
      ubuntu.vm.network "private_network", ip: "192.168.50.2"
      ubuntu.vm.hostname = "master"
      ubuntu.vm.provision "ansible" do |ansible|
         ansible.playbook = "deploy.yaml"
         ansible.host_vars= {
		"worker1" => {"ansible_user" => "ansiuser", "ansible_ssh_pass" => "ansiuser" },
		"worker2" => {"ansible_user" => "ansiuser", "ansible_ssh_pass" => "ansiuser" }
	}
      end
  end 


end
