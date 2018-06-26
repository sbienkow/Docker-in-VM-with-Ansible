# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "generic/ubuntu1604"

	config.vm.network :public_network, :bridge => 'enp0s31f6', :dev => 'enp0s31f6'

  config.vm.provider :libvirt do |libvirt|
		libvirt.memory = 2048
		libvirt.cpus = 2
		libvirt.machine_virtual_size = 40
		libvirt.storage :file, :size => '10G'
	end

  config.vm.provision "shell", inline: 'echo "Start configuration."'
  # config.vm.provision "shell", inline: 'echo -e "rootpass\nrootpass" | passwd root'
  config.vm.provision "shell", inline: 'ln -s /usr/bin/python3 /usr/bin/python'
  config.vm.provision "shell", inline: 'echo "End shell configuration"'

  config.vm.provision "ansible" do |ansible|
    ansible.limit = "all"
    ansible.playbook = "provision_vm.yml"
  end

	# config.vm.provision "file", source: "./daemon.json",  destination: "~vagrant/daemon.json"
	# config.vm.provision "file", source: "./docker-thinpool.profile",  destination: "~vagrant/docker-thinpool.profile"

	# # Probably should use ansible for it instead :/
	# config.vm.provision "shell", inline: <<-SHELL
	# 	apt-get update > /dev/null
	# 	apt-get dist-upgrade -y > /dev/null
	# 	apt-get update > /dev/null
	# 	apt-get upgrade > /dev/null
	# 	apt-get install -y systemd
	# 	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
	# 	add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu  $(lsb_release -cs)  stable"
  #
  #   # create partition, physical volume and then volume group
	#  	(echo n; echo p; echo 1; echo "2048"; echo +5000M; echo w; echo q) | fdisk /dev/vda
  #   pvcreate /dev/vda1
  #   vgcreate docker /dev/vda1
  #   lvcreate --wipesignatures y -n thinpool docker -l 95%VG
  #   lvcreate --wipesignatures y -n thinpoolmeta docker -l 1%VG
  #   lvconvert -y --zero n -c 512K --thinpool docker/thinpool --poolmetadata docker/thinpoolmeta
  #   mkdir -p /etc/lvm/profile/
  #   cp -f ~vagrant/docker-thinpool.profile /etc/lvm/profile/docker-thinpool.profile
  #   lvchange --metadataprofile docker-thinpool docker/thinpool
  #   lvs -o+seg_monitor
  #
	# 	apt-get install -y docker-ce
  #   systemctl stop docker
  #
  #
  #   systemctl stop docker
	# 	cp -f ~vagrant/daemon.json /etc/docker/daemon.json
  #   systemctl start docker
  #
  #   echo "\n\n\nSetup finished"
  #
  #   docker run --name docker-nginx -p 80:80 -d nginx
  #
	#  SHELL

end
