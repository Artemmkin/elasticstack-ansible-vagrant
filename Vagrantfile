Vagrant.require_version ">= 1.8.6"
Vagrant.configure("2") do |config|
  config.vm.define "elk" do |elk|
    elk.vm.box = "ubuntu/trusty64"
    elk.vm.hostname = "elk"

    elk.vm.network :forwarded_port, guest: 5601, host: 5601
    elk.vm.network :forwarded_port, guest: 9200, host: 9200
    elk.vm.network :private_network, ip: "10.37.129.10"
    elk.vm.synced_folder "elastic-stack-showcase/", "/opt/elastic-stack-plays/"

    elk.vm.provider :virtualbox do |vb|
      vb.memory = 3200
      vb.name = "elk"
    end

    elk.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "/opt/elastic-stack-plays/elk.yml"
      #  ansible.verbose = "vvv"
    end
  end

  config.vm.define "web" do |web|
    web.vm.box = "ubuntu/trusty64"
    web.vm.hostname = "web"

    # web.vm.network :forwarded_port, guest: 7000, host: 7000
    web.vm.network :forwarded_port, guest: 80, host: 80
    web.vm.network :private_network, ip: "10.37.129.20"
    web.vm.synced_folder "elastic-stack-showcase/", "/opt/elastic-stack-plays/"

    web.vm.provider :virtualbox do |vb|
      vb.memory = 2000
      vb.name = "web"
    end

    web.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "/opt/elastic-stack-plays/web.yml"
      #  ansible.verbose = "vvv"
    end
  end
end
