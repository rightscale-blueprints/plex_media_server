Vagrant::Config.run do |config|

  # name of vagrant box
  config.vm.box = "plex_media_server"

  # forward guest port 32400 to host port 32401 (PMS web interface)
  # accessible by http://localhost:32401/manage
  config.vm.forward_port 32400, 32401
  
  # upgrade chef to latest known 0.10
  config.vm.provision :shell, :inline => 'gem list | grep chef | grep 10.26.0 || gem install chef -v 10.26.0 --no-rdoc --no-ri'
  
  # chef-solo provisioning
  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = 'cookbooks'
    chef.json.merge!(JSON.parse(File.read('node.json')))
    chef.run_list = JSON.parse(File.read('node.json'))['run_list']
    #chef.run_list = []
    #chef.log_level = :debug
  end

end