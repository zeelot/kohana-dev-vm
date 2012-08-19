Vagrant::Config.run do |config|
  config.vm.box = "dev-vm-2.0"
  config.vm.box_url = "https://zeelot.s3.amazonaws.com/dev-vm-2.0-base.box"

  # Boot with a GUI so you can see the screen. (Default is headless)
  # config.vm.boot_mode = :gui

  # Assign this VM to a host only network IP, allowing you to access it
  # via the IP.
  config.vm.network :hostonly, "33.33.33.10"
  config.vm.network :bridged

  # Forward a port from the guest to the host, which allows for outside
  # computers to access the VM, whereas host only networking does not.
  config.vm.forward_port 80, 8080

  config.vm.share_folder("web-app", "/home/vagrant/web-app", "../", :owner => "vagrant")

  config.vm.provision :chef_solo do |chef|
    # This path will be expanded relative to the project directory
    chef.cookbooks_path = "cookbooks"

    chef.add_recipe("vagrant_main")
    # Uncomment the recipes you would want this app to use
    chef.add_recipe("vagrant_main::phing")
    chef.add_recipe("vagrant_main::mysql")
    # chef.add_recipe("vagrant_main::rabbitmq")
    chef.json = {
      "xdebug" => {
        "remote_enable" => "1",
        "remote_host" => "33.33.33.1"
      },
      # You can configure the VM with a few custom options.
      # Only modify the options below if the defaults don't suit your needs.
      "app" => {
      # Server name used in the apache virtualhost (default is "localhost")
      # "server_name" => "localhost",
      # aliases used in the apache virtualhost (default is ["*.localhost"])
      # "server_aliases" => ["*.localhost"]
      # The docroot in the VM where the app is (default is "/home/vagrant/web-app/httpdocs")
      # You might want to alter this if you don't keep public files in an httpdocs directory
        "docroot" => "/home/vagrant/web-app"
      }
    }
  end
end