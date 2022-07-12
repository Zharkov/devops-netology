Vagrant.configure("2") do |config|
  config.vm.network "forwarded_port", guest: 19999, host: 19999
  config.vm.box = "bento/ubuntu-20.04"
  config.vm.provider "virtualbox" do |v|
    v.name = "my_VM"
  end
end


