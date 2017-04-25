Vagrant.configure("2") do |config|

	config.vm.define "fileserver" do |fileserver|
		fileserver.vm.box = "bento/ubuntu-16.04"
		fileserver.vm.network "private_network", ip: "192.168.33.20"
		fileserver.vm.synced_folder ".", "/vagrant", disabled: true
	end

	config.vm.define "gitserver" do |gitserver|
		gitserver.vm.box = "bento/ubuntu-16.04"
		gitserver.vm.network "private_network", ip: "192.168.33.30"
		gitserver.vm.synced_folder ".", "/vagrant", disabled: true
	end

	config.vm.define "acs" do |acs|
		acs.vm.box = "bento/ubuntu-16.04"
		acs.vm.network "private_network", ip: "192.168.33.10"
		acs.vm.synced_folder ".", "/vagrant", disabled: true
		acs.vm.synced_folder "acs/", "/vagrant"

		acs.vm.provision :ansible_local do |ansible|
			ansible.install_mode = "default"
			# ansible.version = "latest"
			ansible.inventory_path = "inventory"
			ansible.playbook = "cluster.yaml"
			ansible.limit = "all"
		end
	end
end
