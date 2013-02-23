Vagrant::Config.run do |config|
  config.vm.box = "dev-vm-3.0-64bit"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.network :hostonly, "33.33.33.10"
  # config.vm.network :bridged
  # config.vm.boot_mode = :gui

  config.vm.forward_port 80, 8080

  config.vm.share_folder("app", "/home/vagrant/app", "../", :owner => "vagrant")

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"
    chef.roles_path = "roles"
    chef.add_role("app-kohana-dev")
  end
end