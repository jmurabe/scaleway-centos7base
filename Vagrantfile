# -*- mode: ruby -*-
# vi: set ft=ruby :

#.envにて各種設定(vagrantのpluginとしてdotenvが必要) 
Dotenv.load

Vagrant.configure("2") do |config|
  if ENV['TARGET'] == 'scaleway'
    config.vm.provider :scaleway do |scaleway, override|	#要vagrant-scaleway plugin
      scaleway.token = ENV['SCALEWAY_TOKEN']
      scaleway.organization = ENV['SCALEWAY_ORG']
      scaleway.commercial_type = 'VC1S'
      scaleway.image = '9103368e-4fab-4243-aa8d-18121796c086' #CentOS 7.3
      #scaleway.volumes = [
      #  { id: 'ADDITIONAL_VOLUME_UUID' },
      #  { size: 50_000_000_000 }
      #]

      override.ssh.private_key_path = ENV['SCALEWAY_PKEY']
      override.nfs.functional = false
    end
  else
    # ENV['TARGET']はboxの指定(provisioningがCentOS7系前提なので注意)
    config.vm.provider :virtualbox do |vb|
      vb.customize ["setextradata", :id, "VBoxInternal/Devices/VMMDev/0/Config/GetHostTimeDisabled", 0]
    end
    config.vm.box = ENV['TARGET']
    config.vbguest.auto_update = false
    #config.vm.network :forwarded_port, guest: 80, host: 8001
    #config.vm.network :forwarded_port, guest: 3000, host: 3001
    config.vm.network :private_network, ip: '192.168.66.10'
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    #ansible.verbose = "extra"
    ansible.limit = 'all'
  end
end
