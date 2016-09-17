Vagrant.configure("2") do |config|
  config.ssh.forward_agent = true
  config.vm.provider "virtualbox" do |v, override|
    override.vm.box_url = "https://github.com/pilvia/stax/releases/download/b1/stax_b1.box"
    override.vm.box = "stax_b1"
  end
  config.vm.define "magento" do |server|
    server.vm.network :forwarded_port, guest: 80, host:8080
    server.vm.network :forwarded_port, guest: 443, host:8443
    server.vm.network :forwarded_port, guest: 22, host: 12400, id: 'ssh'
    server.vm.synced_folder "./site", "/srv/development", type: "nfs"
    server.vm.network "private_network", type: "dhcp"
    server.vm.hostname = "magento"

    # patch for issue https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Fmitchellh%2Fvagrant%2Fissues%2F6793%23issuecomment-172408346&sa=D&sntz=1&usg=AFQjCNFDCTZpMVSvd5vNn6OjoQULPY-djA
    # remove when 1.8.2 in use
    config.vm.provision "shell" do |s|
        s.inline = '[[ ! -f $1 ]] || grep -F -q "$2" $1 || sed -i "/__main__/a \\    $2" $1'
        s.args = ['/usr/local/bin/ansible-galaxy', "if sys.argv == ['/usr/local/bin/ansible-galaxy', '--help']: sys.argv.insert(1, 'info')"]
    end
    config.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "ansible/magento.yml"
    end
  end
  config.vm.define "wordpress" do |server|
    server.vm.network :forwarded_port, guest: 80, host:8080
    server.vm.network :forwarded_port, guest: 443, host:8443
    server.vm.network :forwarded_port, guest: 22, host: 12400, id: 'ssh'
    server.vm.synced_folder "./site", "/srv/development", type: "nfs"
    server.vm.network "private_network", type: "dhcp"
    server.vm.hostname = "wordpress"

    # patch for issue https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Fmitchellh%2Fvagrant%2Fissues%2F6793%23issuecomment-172408346&sa=D&sntz=1&usg=AFQjCNFDCTZpMVSvd5vNn6OjoQULPY-djA
    # remove when 1.8.2 in use
    config.vm.provision "shell" do |s|
        s.inline = '[[ ! -f $1 ]] || grep -F -q "$2" $1 || sed -i "/__main__/a \\    $2" $1'
        s.args = ['/usr/local/bin/ansible-galaxy', "if sys.argv == ['/usr/local/bin/ansible-galaxy', '--help']: sys.argv.insert(1, 'info')"]
    end
    config.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "ansible/wordpress.yml"
    end
  end


end
