Vagrant.configure("2") do |config|
  ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
  config.ssh.keys_only = false
  config.ssh.forward_agent = true
# Vagrant::Config.run do |config|
#   config.vm.network :bridged
# end
#   (1..2).each do |server_id|
  config.vm.define :web do |web|
    web.vm.box = "ubuntu/xenial64"
    web.vm.hostname = "web"
    web.vm.network "private_network", ip: "192.168.10.10"
    web.vm.network "public_network", bridge: 'eno1'
    web.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512"]
    end
    # config.vm.provision :ansible do |ansible|
    #   ansible.playbook = "setup_web.yml"
    # end
    web.vm.provision "shell" do |s|
    #  ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
      SHELL
    end
  end
  config.vm.define :datab do |datab|
    datab.vm.box = "ubuntu/xenial64"
    datab.vm.hostname = "datab"
    datab.vm.network "private_network", ip: "192.168.10.11"
    datab.vm.network "public_network", bridge: 'eno1'
    datab.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512"]
    end
    # config.vm.provision :ansible do |ansible|
    #   ansible.playbook = "setup_datab.yml"
    # end
    datab.vm.provision "shell" do |s|
    #  ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
      SHELL
    end
  end
end
