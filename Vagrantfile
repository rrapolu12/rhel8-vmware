GENERICE_RHEL8 = "generic/rhel8"
GENERICE_RHEL8_URL = "https://app.vagrantup.com/generic/boxes/rhel8"

JAVA8VM_01_IP = "10.0.50.41"

Vagrant.configure("2") do |config|
  config.vm.box = GENERICE_RHEL8
  config.vm.box_url = GENERICE_RHEL8_URL

  #################### Create a VM with JDK installed #######################
  config.vm.define "java8vm01" do |subconfig|
    subconfig.vm.box = GENERICE_RHEL8
    subconfig.vm.box_url = GENERICE_RHEL8_URL
    subconfig.vm.hostname = "java8vm01.local"
    subconfig.vm.network :private_network, ip: JAVA8VM_01_IP

    subconfig.vm.provider "vmware_desktop" do |vmware|
      # Customize the amount of memory on the VM:
      vmware.memory = "1024"
      vmware.cpus = "1"
      # Enable promiscuous mode
      vmware.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
    end
    ## Now Provision Software Using Ansible
    subconfig.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/jdk8-1-playbook.yml"
      ansible.verbose = "vvv"
      ansible.extra_vars = {
        appName: 'java8vm01'
      }
    end
  end

end