# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

$step1 = 'echo "Step one was run." > custom_log.txt'

$step2 = 'echo "Step two was also run." >> custom_log.txt'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "trusty64"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  BASIC_ONLY = ENV['BASIC_ONLY']
  # package machine
  # set the packaged machine name here
  if BASIC_ONLY
    puts "Doing only step 1 of the provisioning"
    config.vm.provision :shell, inline: $step1
  else
    if system("vagrant box list | grep -q custom_base_box")
      puts "Doing only step 2 of the provisioning"
      config.vm.box = "custom_base_box"
      config.vm.box_url = nil
      config.vm.provision :shell, inline: $step2
    else
      puts "Doing both step 1 and 2 of the provisioning"
      config.vm.provision :shell, inline: "#{$step1}\n#{$step2}"
    end
  end


  config.vm.hostname = "custom.dev"
  config.vm.network "private_network", ip: "192.168.1.77"

  #The ssh port
  config.vm.network :forwarded_port, guest: 22, host: 2224, auto_correct: true, id: "ssh"

  #The development server port
  config.vm.network :forwarded_port, guest: 7778, host: 7778, auto_correct: true

  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--memory", 512]
    v.name = "CUSTOM_vm"
  end

end
