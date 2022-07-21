$mach_quant = 2

Vagrant.configure("2") do |config|
 
  config.vm.provider "virtualbox" do |vb|
  config.vm.box = "bento/ubuntu-20.04"
 end

(1..$mach_quant).each do |i|
    config.vm.define "node#{i}" do |node|
        node.vm.network "public_network", ip: "192.168.0.#{24+i}"
        node.vm.hostname = "node#{i}"
    end
end
  
end 
