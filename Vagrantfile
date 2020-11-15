# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure("2") do |config|
    (1..2).each do |i|
        config.vm.define "server#{i}" do |server|
            server.vm.box = "generic/centos7"
            server.vm.hostname = "server#{i}"

            server.vm.provider :libvirt do |libvirt|
                libvirt.cpus = 1
                libvirt.memory = 512
                libvirt.storage :file, :size => '1G', :path => 'base-cluster_sbd_shared.raw', :allow_existing => true, :shareable => true, :type => :raw
                libvirt.storage :file, :size => '1G', :path => 'base-cluster_data_shared.raw', :allow_existing => true, :shareable => true, :type => :raw
            end

            server.vm.provision :ansible do |ansible|
                ansible.playbook = 'provision.yml'
                ansible.compatibility_mode = '2.0'
            end
        end
    end
end
