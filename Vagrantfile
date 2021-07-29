# -*- mode: ruby -*-
# vi: set ft=ruby :

# Set number of servers
servers = 2

Vagrant.configure("2") do |config|
    (1..servers).each do |i|
        config.vm.define "server#{i}" do |server|
            server.vm.box = "generic/debian10"
            server.vm.hostname = "server#{i}"

            server.vm.provider :libvirt do |libvirt|
                libvirt.cpus = 1
                libvirt.memory = 512
                libvirt.storage :file, :size => '1G', :path => 'base-cluster_sbd_shared.raw', :allow_existing => true, :shareable => true, :type => :raw
                libvirt.storage :file, :size => '1G', :path => 'base-cluster_data_shared.raw', :allow_existing => true, :shareable => true, :type => :raw
            end

            if i == servers
                server.vm.provision :ansible do |ansible|
                    ansible.limit = "all"
                    ansible.playbook = 'provision.yml'
                    ansible.compatibility_mode = '2.0'
                end
            end
        end
    end
end
