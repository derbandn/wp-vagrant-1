
vm_synced_folder="/usr/local/cookbooks"
local_cookbooks_path="cookbooks"

# Vagrant::Config.run do |config|
#   config.vm.forward_port 80, 8080
# end



Vagrant.configure("2") do |config|
   config.vm.provision "shell", inline: "sudo setenforce permissive && iptables -F"
   config.librarian_chef.cheffile_dir = "librarian-chef"

  config.vm.define "test1" do |t1|
    t1.vm.box = "test1/centos7_1.box"
    t1.vm.hostname="test1-centos7"
    t1.vm.synced_folder "cookbooks", vm_synced_folder
    t1.vm.network "private_network", ip: "192.168.56.110" 
    t1.vm.network "forwarded_port", guest: 80, host: 8080
    
      
    t1.vm.provision "chef_solo" do |chef|
      chef.roles_path="roles"
      chef.add_role("test1")
      chef.provisioning_path='/tmp/chef-solo'
      chef.cookbooks_path = "librarian-chef/cookbooks"
      chef.verbose_logging= "true"
    end
    
    
    t1.vm.provision "shell",inline: 'sudo ln -s /opt/VBoxGuestAdditions-4.3.10/lib/VBoxGuestAdditions /usr/lib/VBoxGuestAdditions' 
    
    t1.vm.provider :virtualbox do |vb|
      vb.name = "test1-centos7"
    end   
  end



config.vm.define "test2_db" do |t2|
    t2.vm.box = "test2/centos7_db.box"
    t2.vm.hostname="test2-centos7-db"
    t2.vm.synced_folder "cookbooks", vm_synced_folder
    t2.vm.network "private_network", ip: "192.168.56.111"
      
    t2.vm.provision "chef_solo" do |chef|
      chef.roles_path="roles"
      chef.add_role("test2")
      chef.provisioning_path='/tmp/chef-solo'
      chef.cookbooks_path = "cookbooks"
      chef.verbose_logging= "true"
    end
    
    
    t2.vm.provision "shell",inline: 'sudo ln -s /opt/VBoxGuestAdditions-4.3.10/lib/VBoxGuestAdditions /usr/lib/VBoxGuestAdditions' 
    
    t2.vm.provider :virtualbox do |vb|
      vb.name = "test2-centos7-db"
    end   
  end


end




