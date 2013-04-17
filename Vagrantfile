require 'vagrant-ansible'

Vagrant::Config.run do |config|
  config.vm.box     = "precise32"
  #config.vm.box_url = "http://files.travis-ci.org/boxes/bases/oneiric32_base.box"

  config.vm.forward_port 80, 8085
  
  config.vm.customize ["modifyvm", :id, "--memory", "512"]

  # This is only necessary if your CPU does not support VT-x or you run virtualbox
  # inside virtualbox
  config.vm.customize ["modifyvm", :id, "--vtxvpid", "off"]

  # You can adjust this to the amount of CPUs your system has available
  config.vm.customize ["modifyvm", :id, "--cpus", "1"]

  config.vm.provision :ansible do |ansible|
    # point Vagrant at the location of your playbook you want to run
    ansible.playbook = "setup-devserver.yml"

    # the Vagrant VM will be put in this host group change this should
    # match the host group in your playbook you want to test
    ansible.hosts = "dev-servers"

    # Share this folder with in our vagrant home directory
    config.vm.network :hostonly, '11.0.0.10'  
    config.vm.share_folder("v-root", "/vagrant", ".", :nfs => true)
  end
end