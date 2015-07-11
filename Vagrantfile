# vagrant init ubuntu/trusty64

Vagrant.configure("2") do |config|
    config.vm.box = "trusty64"
    config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

    config.vm.network :private_network, ip: "192.168.42.10"

    config.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--memory", 1024]
        v.customize ["modifyvm", :id, "--name", "blog-docker-compose"]
    end

    config.vm.provision :docker do |d|
        d.build_image "/vagrant/docker/base", args: "-t link0/base"
    end

    config.vm.provision :docker_compose, yml: "/vagrant/docker-compose.yml", run: "always"

end
