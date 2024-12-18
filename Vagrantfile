Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2004"
  (1..2).each do |id|
    config.vm.define "server-#{id}" do |node|
      node.vm.hostname = "server-#{id}"
      node.vm.network "private_network", bridge: ["eno1"] ,ip: "192.168.56.#{id+200}"

      node.vm.provider "virtualbox" do |vb|
        vb.name= "server-#{id}"
        vb.memory = "1024"
        vb.cpus = 2
      end

      node.vm.provision "ansible" do |ansible|
        ansible.playbook = "./main.yaml"
        ansible.groups = {
          "group1" => ["server-1"],
          "group2" => ["server-2"]}
      end
    end
  end
end
