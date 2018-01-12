# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
	4.times do |n|
		config.vbguest.iso_path = "/Applications/VirtualBox.app/Contents/MacOS/VBoxGuestAdditions.iso"
		config.vbguest.auto_update = false
		config.ssh.insert_key = true
		config.ssh.username = 'vagrant'
		config.ssh.password = 'vagrant'
		config.vm.define "node"+(1+n).to_s do |cc|
    			cc.vm.host_name = "node" + (1+n).to_s
    			cc.vm.network :private_network, ip: "10.10.10.1" + n.to_s
					if cc.vm.hostname == "node1" then
						cc.vm.network "forwarded_port", guest: 3306, host: 3307					
						cc.vm.box = "bento/centos-7.4"
						cc.vm.box_check_update = true
						cc.vm.provider :virtualbox do |vb|
								vb.gui = false
								vb.memory = "1024"
								vb.name = "node"+(1+n).to_s
						end
					end
					if cc.vm.hostname == "node2" then
						 cc.vm.network "forwarded_port", guest: 3306, host: 3308					
						 cc.vm.box = "bento/centos-7.4"
						 cc.vm.box_check_update = true
						 cc.vm.provider :virtualbox do |vb|
								vb.gui = false
								vb.memory = "1024"
								vb.name = "node"+(1+n).to_s
						end
					end
					if cc.vm.hostname == "node3" then
						 cc.vm.network "forwarded_port", guest: 3306, host: 3309					
						 cc.vm.box = "bento/centos-7.4"
						 cc.vm.box_check_update = true
						 cc.vm.provider :virtualbox do |vb|
								vb.gui = false
								vb.memory = "1024"
								vb.name = "node"+(1+n).to_s
						end
					end				
					if cc.vm.hostname == "node4" then
						 cc.vm.network "forwarded_port", guest: 3306, host: 3310					
						 cc.vm.box = "bento/centos-7.4"
						 cc.vm.box_check_update = true
						 cc.vm.provider :virtualbox do |vb|
								vb.gui = false
								vb.memory = "1024"
								vb.name = "node"+(1+n).to_s
						end
					end			
		end
	end
end
