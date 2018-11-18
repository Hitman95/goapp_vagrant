# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|
 config.env.enable # Enable vagrant-env(.env)
  config.vm.define "goapp-vagrant" do |config|
      config.vm.provider :digital_ocean do |provider, override|
        provider.ssh_key_name = 'Hitman95'        
        override.ssh.private_key_path = '~/.ssh/id_rsa'
        override.vm.box = 'digital_ocean'
        override.vm.box_url = "https://github.com/devopsgroup-io/vagrant-digitalocean/raw/master/box/digital_ocean.box"
        override.nfs.functional = false
        provider.token = ENV['TOKEN']
        provider.image = 'ubuntu-16-04-x64'
        provider.region = 'fra1'
        provider.size = '512mb'
      end

     config.vm.synced_folder ".", "/vagrant", disabled: true

     config.vm.provision "shell",
        inline: "apt update -y && apt install -y python2.7-minimal && update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1"

     config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/app.yml"
     end

  end
end
