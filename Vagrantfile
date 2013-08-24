# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.network :public_network
  # config.vm.network :forwarded_port, guest: 80, host: 8080
  # config.vm.network :private_network, ip: "192.168.33.10"

  src_dir = './sandbox/kumaWP'
  doc_root = '/vagrant_data'
  dump_dir = './dump'
  backup_dir = '/vagrant_backup'

  #Developing Code dir.
  config.vm.synced_folder src_dir, doc_root, :create => true, :owner=> 'vagrant', :group=>'www-data', :extra => 'dmode=775,fmode=775'
  #Exposing the archive
  config.vm.synced_folder dump_dir, backup_dir, :create => true, :owner => 'vagrant', :group => 'vagrant', :extra => 'dmode=775,fmode=755'

  config.vm.provision :chef_solo do |chef|
    # chef.cookbooks_path = ["./cookbooks", "./site-cookbooks"]
    chef.cookbooks_path = "./cookbooks"
    chef.add_recipe "omusubi"
    chef.add_recipe "database::mysql"
    chef.add_recipe "mysql"
    chef.json = {
      doc_root: doc_root,
      mysql: {
        server_root_password: ""
      }
    }
  end
end
