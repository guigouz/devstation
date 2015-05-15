Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty32"

  config.vm.hostname = "devstation.local"

  config.vm.network :private_network, ip: "192.168.56.101"

  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
    v.customize ["modifyvm", :id, "--memory",512]
    v.customize ["modifyvm", :id, "--cpus", "1"]
  end

  config.vm.synced_folder "./webapp", "/var/www/webapp", owner: "www-data", group: "www-data"

  #config.vm.provision :shell, :path => "bootstrap.sh"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "devstation.yml"
  end

  config.vm.provision "shell", inline: "sudo service apache2 restart", run: "always"

end
