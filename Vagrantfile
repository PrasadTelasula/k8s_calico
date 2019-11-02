# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|


  config.vm.provision "shell", path: "bootstrap.sh"



  # Kubernetes Master Server
  config.vm.define "master" do |master|
    master.vm.box = "centos/7"
    master.vm.hostname = "master.k8slocal.com"
    master.vm.network "private_network", ip: "172.32.32.100"
    master.vm.provider "virtualbox" do |v|
      v.name = "master"
      v.memory = 2048
      v.cpus = 2
    end
    master.vm.provision "shell", path: "bootstrap_kmaster.sh"
  end



  NodeCount = 2

  # Kubernetes Worker Nodes
  (1..NodeCount).each do |i|
    config.vm.define "worker#{i}" do |workernode|
      workernode.vm.box = "centos/7"
      workernode.vm.hostname = "worker#{i}.k8slocal.com"
      workernode.vm.network "private_network", ip: "172.32.32.10#{i}"
      workernode.vm.provider "virtualbox" do |v|
        v.name = "k8sworker#{i}"
        v.memory = 1024
        v.cpus = 1
      end
      workernode.vm.provision "shell", path: "bootstrap_kworker.sh"
    end
  end

end
