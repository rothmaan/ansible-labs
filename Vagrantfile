Vagrant.configure("2") do |config|
  servers = [
    {
      :hostname => "db01",
      :box => "generic/centos9s",
      :ip => "192.168.50.101",
    },
    {
      :hostname => "web01",
      :box => "generic/centos9s",
      :ip => "192.168.50.102",
    },
    {
      :hostname => "web02",
      :box => "generic/centos9s",
      :ip => "192.168.50.103",
    },
    {
      :hostname => "proxy",
      :box => "centos/8",
      :ip => "192.168.50.104",
    }
  ]

  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
      node.vm.box = machine[:box]
      node.vm.hostname = machine[:hostname]
      node.vm.network :private_network, ip: machine[:ip]
      node.vm.provision "ansible", playbook: "useradd.yaml"

      node.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--memory", 512]
        # Use a unique VM name for VirtualBox to avoid directory conflicts
        v.customize ["modifyvm", :id, "--name", "#{machine[:hostname]}_#{machine[:ip]}"]
      end
    end
  end
end

