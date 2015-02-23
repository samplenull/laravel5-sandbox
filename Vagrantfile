Vagrant.configure("2") do |config|

    config.vm.box = "parallels/ubuntu-14.04"
    config.vm.box_url = "https://vagrantcloud.com/parallels/boxes/ubuntu-14.04"
    config.vm.network :private_network, ip: "192.168.33.99" #
    config.ssh.forward_agent = true

   config.vm.provider :parallels do |v|
    v.name = "php5_sandbox_local"
    v.update_guest_tools = true
    v.optimize_power_consumption = false
    v.cpus = 2
    v.memory = 2048
  end

  config.vm.synced_folder "./app/", "/vagrant", id: "vagrant-root"

   
    #############################################################
    # Ansible provisioning (you need to have ansible installed)
    #############################################################
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/playbook.yml"
        ansible.inventory_path = "ansible/inventories/dev"
        ansible.limit = 'all'
        ansible.extra_vars = {
            private_interface: "192.168.33.99",
            hostname: "default"
        }
    end
    
end
