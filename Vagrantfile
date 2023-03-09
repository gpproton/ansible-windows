timeout = 1200
nodes = [
  { :hostname => 'virt-00',  :ip => '10.10.0.10', :box => 'jborean93/WindowsServer2022', :ram => 3072 , :cpus => 2 }
]

Vagrant.configure("2") do |config|
  nodes.each do |node|
    config.vm.define node[:hostname] do |nodeconfig|
      nodeconfig.vm.boot_timeout = timeout
      nodeconfig.vm.box = node[:box]
      nodeconfig.vm.hostname = node[:hostname] + ".sv.easy"
      nodeconfig.vm.network :private_network, ip: node[:ip]
      nodeconfig.vm.provider :libvirt do |vb|
        vb.memory = node[:ram]
        vb.cpus = node[:cpus]
      end
      memory = node[:ram]
      nodeconfig.vm.provider :virtualbox do |vb|
        vb.name = node[:hostname]
        vb.linked_clone = true
        vb.memory = node[:ram]
        vb.cpus = node[:cpus]
        vb.customize [
          "modifyvm", :id,
          "--cpuexecutioncap", "50",
          "--memory", memory.to_s,
        ]
      end
    end
  end
end