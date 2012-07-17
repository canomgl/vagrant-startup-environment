# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'Vagrant/vagrant-puppet-local/lib/puppet-local'  

Vagrant::Config.run do |config|

  config.vm.box     = "CentOS-6.3-x86_64-minimal"
  config.vm.box_url = "https://dl.dropbox.com/u/7225008/Vagrant/CentOS-6.3-x86_64-minimal.box"

  config.vm.customize do |vm|
    vm.name        = "app-name"    
    vm.memory_size = 1024
  end

  config.vm.network :hostonly, "192.168.33.10"

  config.puppet_local.puppet_destroy_path = 'Puppet/manifests/vagrant/destroy.pp'
  config.puppet_local.puppet_up_path      = 'Puppet/manifests/vagrant/up.pp'

  config.vm.provision :puppet, 
      :module_path => "Puppet/modules",
      :options => ["--fileserverconfig=/vagrant/PuppetRemote/conf/fileserver.conf", ] do |puppet|
    puppet.manifests_path = "Puppet/manifests"
    puppet.module_path    = "Puppet/modules"
    puppet.manifest_file  = "default.pp"
  end

  config.vm.share_folder "app-name", "/var/www/vhosts/default/localhost.dev/httpdocs", ".", :nfs => false 

end